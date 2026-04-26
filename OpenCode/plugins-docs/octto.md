# octto

> النوع: Browser UI for AI Brainstorming  
> الـ Repo: https://github.com/vtemian/octto

---

## 1. إيه هي الإضافة دي؟

**octto** هي plugin بتدي الـ OpenCode **interactive browser UI** للـ AI brainstorming. بدل ما تتعامل مع الـ AI من الـ terminal بس، بتفتحلك واجهة في الـ browser فيها:

- **Multi-question forms** — تجاوب على كذا سؤال في وقت واحد
- **Visual interaction** — أسهل من الـ terminal للـ brainstorming الطويل
- **Interactive UI** — رسوم بيانية، forms، checkboxes، إلخ

تخيلها كـ "Notion for AI Brainstorming" — بتديك space مرئي للتفكير مع الـ AI.

### مرتبطة بـ micode:
الـ plugin ده من نفس صاحب `micode` (الـ Brainstorm → Plan → Implement workflow). لو بتستخدم micode، octto هي الـ UI الخاصة بيها.

---

## 2. في ماذا تستخدم؟

استخدمها عشان:

- ✅ **brainstorming sessions طويلة** بتحتاج visual interaction
- ✅ **multi-question forms** بدل ما الـ AI يسألك سؤال سؤال
- ✅ **planning visual** بـ checkboxes و dropdowns
- ✅ **structured exploration** للأفكار قبل الـ implementation
- ✅ **عرض البدائل** بشكل بصري

### السيناريو النموذجي:

```
أنت: "I want to build a SaaS dashboard"

octto: [بيفتحلك form فيه]
  - What's your target audience? [dropdown]
  - Authentication method? [radio buttons]
  - Database choice? [checkboxes]
  - Real-time features needed? [yes/no]
  - Tech stack preference? [text input]
  
[بتجاوب كل ده مرة واحدة]

AI: [بيرتب البدائل بناءً على إجاباتك]
```

---

## 3. كيف تستخدم؟

### التثبيت

في `~/.config/opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["octto"]
}
```

### التشغيل

الـ plugin بيشتغل web server محلي (عادةً على port معين).

```bash
# شغل OpenCode
opencode

# لما تطلب brainstorming task، الـ plugin بيفتحلك URL
# افتح الـ URL في الـ browser
```

### مع micode:

الـ micode بيستخدم octto كـ UI:

```
أنت: "Help me brainstorm a new feature"

micode: [بيستخدم octto لعرض الـ form]
[الـ browser بيفتح بـ form interactive]
```

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ بتعمل **brainstorming لمشاريع جديدة**
- ✅ محتاج **planning visual** قبل الـ implementation
- ✅ بتعمل **multi-step questionnaires** مع الـ AI
- ✅ بتحب الـ **GUI** أكتر من الـ terminal
- ✅ بتشتغل مع **micode** workflow
- ✅ شغلك بيحتاج **decision-making معقد** فيه trade-offs كتير

### متستخدمهاش لو:
- ❌ شغلك في الـ terminal بس ومش حابب browser
- ❌ بتعمل **quick tasks** مش محتاجة planning
- ❌ بتشتغل في بيئة **headless** (server بدون GUI)
- ❌ بتفضل الـ **command-line workflow**
- ❌ مش بتعمل brainstorming كتير

---

## ⚠️ ملاحظات مهمة

### Browser Requirement:
محتاج browser شغال على الجهاز عشان تستخدم الـ UI.

### الـ Local Server:
الـ plugin بيشغل web server محلي على بورت معين. تأكد إن البورت ده مش متستخدم.

### Privacy:
الـ data بتفضل محلية على جهازك (الـ web server محلي مش remote).

### مع micode:
الـ plugin ده مصمم primarily للشغل مع `micode`. تقدر تستخدمه لوحده، بس قوته الحقيقية لما بيكون في combo معاها.

---

## 🔗 روابط مفيدة

- Repo: https://github.com/vtemian/octto
- micode (المشروع الشقيق): https://github.com/vtemian/micode
