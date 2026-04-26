# opencode-morph-fast-apply (JRedeker)

> النوع: Code Editing Acceleration Plugin  
> الـ Repo: https://github.com/JRedeker/opencode-morph-fast-apply

---

## 1. إيه هي الإضافة دي؟

**opencode-morph-fast-apply** هي plugin بتسرع تعديل الكود **10x** عن طريق Morph Fast Apply API. الفكرة الأساسية:

- بدل ما الـ AI agent يكتب الفايل **كله من الأول** عشان يعدل سطر
- بيستخدم **lazy edit markers** — يعني بيقول "هنا اتغير، الباقي زي ما هو"
- Morph API بياخد الـ markers دي ويطبق التعديل بسرعة على الفايل الأصلي

### المشكلة اللي بيحلها:

```
بدون Morph:
  Agent: [يقرا الفايل كله 500 سطر]
  Agent: [يكتب الفايل كله 505 سطر بالتعديل]
  Cost: 1000+ tokens

مع Morph:
  Agent: [يقرا الفايل]
  Agent: [يكتب lazy edit: "+ added new function here"]
  Morph: [يطبق التعديل على الفايل الأصلي]
  Cost: ~100 tokens
```

---

## 2. في ماذا تستخدم؟

استخدمها عشان:

- ✅ **توفير 10x من الـ tokens** في الـ file edits
- ✅ **سرعة عالية** في تعديل الفايلات الكبيرة
- ✅ **lazy edit markers** — تعديل ذكي بدون كتابة الفايل كله
- ✅ **دقة في التعديل** — Morph specialized في الـ apply task ده
- ✅ **توفير الـ time** اللي الـ agent بيقعد يكتب فيه فايلات كبيرة

### النموذجي:

تخيل Vue component بتاعك 800 سطر، عايز تضيف method جديد:

```
بدون Morph: الـ agent بيكتب 800+ سطر تاني
مع Morph: الـ agent بيكتب lazy markers بـ 50 سطر بس
```

---

## 3. كيف تستخدم؟

### الخطوة 1: الحصول على Morph API Key

روح لـ [morphllm.com](https://morphllm.com) وسجل واخد API key.

### الخطوة 2: التثبيت

في `~/.config/opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["github:JRedeker/opencode-morph-fast-apply"]
}
```

### الخطوة 3: ضبط الـ API Key

```bash
export MORPH_API_KEY="your-api-key-here"
```

أو في الـ env file بتاع OpenCode.

### الاستخدام:

الـ plugin بيشتغل **automatically** — لما الـ agent يحاول يعدل فايل، الـ Morph plugin بياخد الـ edit و يطبقه بسرعة.

مفيش حاجة تعملها يدوياً، بس ممكن تشوف في الـ logs إن الـ Morph شغال:

```
[INFO] Using Morph Fast Apply for file: src/composables/useAuth.ts
```

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ بتشتغل على **فايلات كبيرة** (300+ سطر)
- ✅ بتعدل **multiple files** في session واحد
- ✅ بتدفع على **API بـ tokens** (Anthropic, OpenAI)
- ✅ شغلك على **Vue components** أو React components كبيرة
- ✅ بتعدل في **base-layer** بتاع Nanosoft (فايلات shared كبيرة)
- ✅ عايز توفير حقيقي في الـ tokens والوقت

### متستخدمهاش لو:
- ❌ بتشتغل على **فايلات صغيرة** (<100 سطر)
- ❌ بتستخدم **free models** (الـ Morph API بيتكلف فلوس)
- ❌ مش عايز **dependency خارجية** على service
- ❌ بتعمل **prototyping** على فايلات قصيرة

---

## ⚠️ ملاحظات مهمة

### التكلفة:
الـ Morph API مدفوع. شوف pricing على [morphllm.com](https://morphllm.com).

### مقارنة مع الـ opencode-morph-plugin الرسمي:

في plugin تاني اسمه `opencode-morph-plugin` من فريق Morph نفسه (`morphllm/opencode-morph-plugin`)، الفرق:

| الجانب | JRedeker (ده) | Morph الرسمي |
|--------|---------------|--------------|
| المميزات | Fast Apply + lazy markers | Fast Apply + WarpGrep + context compaction |
| الـ Maintenance | Community | الفريق الرسمي |
| المميزات الإضافية | Lazy markers focused | شامل أكتر |

لو محتاج المميزات الإضافية، فكر في الـ plugin الرسمي.

### مع Plugins تانية:
- ✅ متوافق مع كل plugins الـ OpenCode التانية
- ✅ بيشتغل بشكل خاص كويس مع `opencode-dynamic-context-pruning` (المزيج بيوفر tokens مضاعفة)

---

## 🔗 روابط مفيدة

- Repo: https://github.com/JRedeker/opencode-morph-fast-apply
- Morph: https://morphllm.com
- الـ Morph الرسمي: https://github.com/morphllm/opencode-morph-plugin
