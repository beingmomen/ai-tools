# @tarquinen/opencode-dcp (Dynamic Context Pruning)

> النوع: Token Optimization Plugin  
> الـ Repo: https://github.com/Opencode-DCP/opencode-dynamic-context-pruning  
> الـ NPM: `@tarquinen/opencode-dcp`  
> الـ Stars: 2.3k+ ⭐

---

## 1. إيه هي الإضافة دي؟

**DCP (Dynamic Context Pruning)** هو plugin بيقلل **استهلاك الـ tokens تلقائياً** عن طريق إدارة ذكية للـ conversation context. الفكرة الأساسية إنه بيشيل الـ tool outputs القديمة اللي مش محتاجها من الـ context قبل ما يبعت الـ request للـ LLM.

⚠️ مهم: الـ session history الأصلي **مش بيتغير** — الـ DCP بيستبدل الـ pruned content بـ placeholders بس قبل إرسال الـ request.

### المكونات الرئيسية:

1. **Compress Tool** — أداة بيستخدمها الموديل عشان يلخص محادثات قديمة بطريقة technical عالية الجودة (أذكى من الـ compaction العادي بتاع OpenCode).

2. **Deduplication** — بيمسح الـ tool calls المتكررة (نفس الأداة بنفس الـ arguments) ويحتفظ بالأخيرة بس.

3. **Purge Errors** — بيشيل الـ inputs الكبيرة من الـ tools اللي حصل فيها errors بعد عدد turns معين (default: 4).

---

## 2. في ماذا تستخدم؟

استخدمها لما تحب:

- ✅ **توفير 30-50% من الـ tokens** في الـ long sessions
- ✅ **منع hallucinations** الناتجة من stale context
- ✅ **التحكم في حجم الـ context window** بشكل ذكي
- ✅ **حماية tool outputs مهمة** من الـ pruning عبر glob patterns
- ✅ **عمل compress يدوي** عبر `/dcp compress`
- ✅ **مراقبة استهلاك الـ tokens** عبر `/dcp context` و `/dcp stats`

### المميزات الفنية:

- **Range Mode** (default) — يضغط مساحات متصلة من المحادثة في summaries
- **Message Mode** (تجريبي) — يضغط رسائل فردية بشكل منفصل
- **Layered Compression** — لما compression جديد يتداخل مع قديم، الـ summary القديم بيتدمج جواه (المعلومات بتتحفظ عبر طبقات)
- **Protected Tools** — تحمي tool outputs معينة من الضغط (افتراضياً: `task`, `skill`, `todowrite`, `todoread`, `compress`, `batch`, `plan_enter`, `plan_exit`, `write`, `edit`)

---

## 3. كيف تستخدم؟

### التثبيت السهل

```bash
opencode plugin @tarquinen/opencode-dcp@latest --global
```

ده هيحط الـ plugin في الـ global config تلقائياً.

### أو يدوياً في `~/.config/opencode/opencode.json`:

```json
{
  "plugin": ["@tarquinen/opencode-dcp@latest"]
}
```

### الإعدادات

اعمل ملف `~/.config/opencode/dcp.jsonc`:

```jsonc
{
  "$schema": "https://raw.githubusercontent.com/Opencode-DCP/opencode-dynamic-context-pruning/master/dcp.schema.json",
  "enabled": true,
  "debug": false,
  
  // إعدادات الـ Compress
  "compress": {
    "mode": "range",           // أو "message" (تجريبي)
    "permission": "allow",     // "allow" / "ask" / "deny"
    "maxContextLimit": 100000, // الحد الأقصى قبل ما يضغط
    "minContextLimit": 50000,  // الحد الأدنى للتذكيرات
    "nudgeFrequency": 5,
    "protectUserMessages": false,
    "protectedTools": []
  },
  
  // الـ Strategies التلقائية
  "strategies": {
    "deduplication": {
      "enabled": true,
      "protectedTools": []
    },
    "purgeErrors": {
      "enabled": true,
      "turns": 4
    }
  }
}
```

### الـ Slash Commands المتاحة

| الأمر | الوظيفة |
|------|---------|
| `/dcp` | عرض الأوامر المتاحة |
| `/dcp context` | عرض breakdown للـ tokens في الـ session الحالي |
| `/dcp stats` | إحصائيات تراكمية لكل الـ sessions |
| `/dcp sweep` | يحذف كل الـ tools من آخر user message |
| `/dcp sweep 10` | يحذف آخر 10 tools بس |
| `/dcp compress [focus]` | يشغل compress مرة واحدة (مع تحديد المحتوى اختياري) |
| `/dcp decompress <n>` | يرجع compression معين بالـ ID |
| `/dcp recompress <n>` | يعيد تطبيق compression رجعته |
| `/dcp manual [on/off]` | يفعل/يطفي الـ manual mode |

### في حالة Models صغيرة:

لو بتستخدم GitHub Copilot models أو local models، قلل الـ limits:

```jsonc
{
  "compress": {
    "maxContextLimit": "80%",  // من الـ context window للموديل
    "minContextLimit": "25%",
    "modelMaxLimits": {
      "openai/gpt-5.3-codex": 120000,
      "anthropic/claude-sonnet-4.6": "80%"
    }
  }
}
```

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ بتعمل long sessions (أكتر من ساعة شغل)
- ✅ بتقرا files كتيرة في نفس الـ session
- ✅ بتشتغل على codebase كبير زي base-layer
- ✅ بتشتغل على API بدفع per-token (Anthropic، OpenAI)
- ✅ بتلاحظ إن الموديل بقا "بيفقد التركيز" في الـ long conversations
- ✅ مرات بتاخد errors من الـ tools وعايز تشيل الـ inputs الكبيرة

### متستخدمهاش لو:
- ❌ بتشتغل على tasks بسيطة وقصيرة
- ❌ بتستخدم providers بـ flat-rate (زي GitHub Copilot per-request)
- ❌ بتستخدم providers بـ uniform pricing (زي Cerebras)
- ❌ في sessions قصيرة الـ overhead مش هيفرق

---

## ⚠️ ملاحظات مهمة

### Trade-off في الـ Caching:
- **بدون DCP**: cache hit rate ~ 90%
- **مع DCP**: cache hit rate ~ 85%

يعني هتفقد شوية من cache reads، بس هتكسب توفير tokens أكبر بكتير في الـ long sessions.

### Manual Mode:
لو حابب تتحكم 100% في الـ pruning، فعّل الـ `manualMode`:

```jsonc
{
  "manualMode": {
    "enabled": true,
    "automaticStrategies": true  // بيخلي dedup و purgeErrors شغالة بس
  }
}
```

### الترخيص: AGPL-3.0

---

## 🔗 روابط مفيدة

- README: https://github.com/Opencode-DCP/opencode-dynamic-context-pruning
- NPM: https://www.npmjs.com/package/@tarquinen/opencode-dcp
- Schema: https://raw.githubusercontent.com/Opencode-DCP/opencode-dynamic-context-pruning/master/dcp.schema.json
