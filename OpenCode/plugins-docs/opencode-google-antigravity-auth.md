# opencode-google-antigravity-auth

> النوع: Auth Plugin (تستخدم موديلات مجانية)  
> الـ Repo: https://github.com/shekohex/opencode-google-antigravity-auth  
> الـ NPM: `opencode-google-antigravity-auth`

---

## ⚠️ تنبيه مهم قبل التثبيت

1. **الـ Repo اتأرشف** في 28 فبراير 2026 (read-only ومش بيتم تطويره).
2. **في تقارير Google بتحظر الحسابات** اللي بتستخدم الـ plugin ده.
3. **Antigravity ToS** بيقول إن الخدمة مش مفروض تتستخدم مع منتجات تانية.

> 🚨 استخدمها على مسؤوليتك الشخصية، ويفضل تستخدم حساب Google مش الأساسي.

---

## 1. إيه هي الإضافة دي؟

**opencode-google-antigravity-auth** هي plugin بيعمل OAuth authentication مع **Google Antigravity** (الـ AI IDE المجاني من Google) عشان تستخدم موديلات Gemini و Claude **بدون ما تدفع** على API credits.

الـ plugin ده fork من `opencode-gemini-auth` بس بمميزات إضافية أقوى.

### الموديلات اللي هتقدر توصلها مجاناً:
- **Gemini 3 Pro** (أقوى موديل من Google للـ reasoning)
- **Gemini 3 Flash** (سريع وذكي)
- **Gemini 2.5 Flash Lite**
- **Claude Sonnet 4.5** (عبر Antigravity proxy)
- **Claude Opus 4.5 with thinking**

---

## 2. في ماذا تستخدم؟

استخدمها لما تحب:

- ✅ **توفير 100% من تكاليف الـ API** (مهم جداً لو ما تقدرش تدفع لـ Google API من مصر)
- ✅ **Multi-Account Load Balancing** — تدوير تلقائي بين حسابات Google متعددة (لحد 10 حسابات)
- ✅ **Endpoint Fallback** — بيجرب 3 endpoints (daily → autopush → prod) لأقصى reliability
- ✅ **Google Search Tool** مدمج — بحث ويب حقيقي مع تحليل URLs و source citations
- ✅ **Cross-Model Conversations** — تنقل بين Gemini و Claude في نفس الـ session مع الحفاظ على thinking blocks
- ✅ **Automatic Token Refresh** — مش هتحتاج تجدد التوكن يدوياً
- ✅ **Interleaved Thinking** للموديلات الـ thinking — Claude بيفكر بين كل tool call والتاني

---

## 3. كيف تستخدم؟

### الخطوة 1: التثبيت

أضف للـ `~/.config/opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["opencode-google-antigravity-auth"]
}
```

### الخطوة 2: تسجيل الدخول

```bash
opencode auth login
```

ثم اختار:
1. الـ Google provider
2. **OAuth with Google (Antigravity)**
3. هيفتحلك browser للموافقة
4. (اختياري) ضيف حسابات إضافية للـ load balancing

### الخطوة 3: إعداد الموديلات (موصى به)

أضف للـ `opencode.json` الـ providers config (موجودة كاملة في الـ README الأصلي):

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["opencode-google-antigravity-auth"],
  "provider": {
    "google": {
      "npm": "@ai-sdk/google",
      "models": {
        "gemini-3-pro-preview": {
          "id": "gemini-3-pro-preview",
          "name": "Gemini 3 Pro",
          "modalities": {
            "input": ["text", "image", "video", "audio", "pdf"],
            "output": ["text"]
          },
          "variants": {
            "high": { 
              "options": { 
                "thinkingConfig": { 
                  "thinkingLevel": "high", 
                  "includeThoughts": true 
                } 
              } 
            }
          }
        },
        "gemini-3-flash": { /* ... */ },
        "gemini-claude-sonnet-4-5-thinking": { /* ... */ },
        "gemini-claude-opus-4-5-thinking": { /* ... */ }
      }
    }
  }
}
```

### الاستخدام اليومي

```bash
# استخدام Gemini 3 Pro
opencode run -m google/gemini-3-pro-preview -p "fix this bug"

# استخدام Claude Opus عبر Antigravity
opencode run -m google/gemini-claude-opus-4-5-thinking -p "review this code"
```

### تحديث الـ Plugin

OpenCode مش بيحدث الـ plugins تلقائياً. عشان تحدث:

```bash
rm -rf ~/.cache/opencode/node_modules/opencode-google-antigravity-auth
opencode
```

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ مش قادر تدفع على Google AI API (مشكلة شائعة في مصر مع الدفع الإلكتروني)
- ✅ محتاج Gemini 3 Pro للـ reasoning المعقد
- ✅ محتاج Claude مجاناً عبر Antigravity proxy
- ✅ بتشتغل على مشاريع heavy-usage محتاجة multi-account rotation
- ✅ محتاج Google Search مدمج في الـ workflow بتاعك
- ✅ بتعمل multimodal input (صور، فيديو، PDF)

### متستخدمهاش لو:
- ❌ عندك اشتراك مدفوع في Google AI Pro/Ultra (استخدم `opencode-gemini-auth` بدالها)
- ❌ مش مستعد لمخاطرة حظر حساب Google
- ❌ بتستخدم plugin `opencode-skills` (في incompatibility — استخدم `openskills` بدالها)
- ❌ شغلك حساس و الـ Google ToS مهم ليك

---

## ⚠️ ملاحظات مهمة

### تعارضات معروفة:
- `opencode-skills` — مش متوافق، استخدم `openskills` بدالها
- لو بتستخدم plugins تانية للـ auth (زي `opencode-gemini-auth` أو `opencode-antigravity-auth`)، هيحصل تعارض

### Image Support:
لازم تضيف الـ `modalities` config للموديل في `opencode.json` تحت `provider.google.models.<model>.modalities.input` يبقى فيه `"image"`.

### Multi-Account Storage:
بيخزن metadata الحسابات في:
```
$XDG_DATA_HOME/opencode/antigravity-accounts.json
```
أو `~/.local/share/opencode/antigravity-accounts.json`

### Debugging:
```bash
opencode --log-level DEBUG --print-logs
```
الـ logs بتبقى في `~/.local/share/opencode/logs/`

---

## 🔗 روابط مفيدة

- README: https://github.com/shekohex/opencode-google-antigravity-auth
- NPM: https://www.npmjs.com/package/opencode-google-antigravity-auth
- Antigravity ToS: https://antigravity.google/terms
