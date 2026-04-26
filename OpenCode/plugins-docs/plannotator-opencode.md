# @plannotator/opencode

> النوع: Interactive Plan Review with Visual Annotation  
> الـ Repo: https://github.com/backnotprop/plannotator/tree/main/apps/opencode-plugin

---

## 1. إيه هي الإضافة دي؟

**@plannotator/opencode** هي plugin بتدي الـ OpenCode قدرة **Interactive Plan Review** مع **Visual Annotation**. الفكرة الأساسية:

- لما الـ AI agent يعمل plan لمهمة كبيرة
- بدل ما تقرأ الـ plan كنص في الـ terminal
- بتحصل على **visual interface** فيها تقدر:
  - تـ annotate (تعلق) على أجزاء معينة
  - تـ approve/reject خطوات
  - تـ share الـ plan مع الفريق (offline)

### الفلسفة:
الـ AI plans أحياناً بتكون طويلة ومعقدة. الـ plugin ده بيخليك **تـ review الـ plan بصرياً** قبل الـ execution، عشان تقدر تـ catch الأخطاء أو الـ misunderstandings مبكراً.

---

## 2. في ماذا تستخدم؟

استخدمها عشان:

- ✅ **مراجعة plans طويلة** بشكل بصري
- ✅ **Annotations على الـ plan** (تعليقات على خطوات معينة)
- ✅ **Private/Offline sharing** — مشاركة الـ plans مع الفريق بدون cloud
- ✅ **Step-by-step approval** — approve كل خطوة لوحدها
- ✅ **التعديل التفاعلي** على الـ plan قبل الـ implementation
- ✅ **توثيق القرارات** اللي اتخذت أثناء الـ planning

### السيناريو النموذجي:

```
أنت: "Refactor the authentication system to use JWT"

AI: [يعمل plan طويل من 15 خطوة]

[plannotator يفتحلك UI:]
✅ Step 1: Audit current auth implementation
✅ Step 2: Create JWT utility module
🤔 Step 3: Replace session-based auth
   └─ [Annotation: "Make sure to keep backward compatibility for 1 month"]
❌ Step 4: Remove old session tables  
   └─ [Annotation: "Don't drop yet, just migrate users"]
✅ Step 5: Update middleware
...

[بتـ approve/reject/comment على كل خطوة]

AI: [يبدأ الـ implementation بناءً على الـ approved plan + annotations]
```

---

## 3. كيف تستخدم؟

### التثبيت

في `~/.config/opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["@plannotator/opencode@latest"]
}
```

### التشغيل

الـ plugin بيشتغل لما الـ AI يحاول يعمل plan:

```bash
opencode

# الـ AI لما يعمل plan كبير:
# > Plan generated. Open in plannotator? (Y/n)
# اضغط Y
# الـ UI بيفتح في browser
```

### الـ UI بتديك:

1. **عرض الـ plan كاملاً** مع steps مرقمة
2. **زرار approval/rejection** لكل step
3. **زرار annotation** لكتابة تعليقات
4. **زرار "Implement"** لما تخلص الـ review
5. **زرار "Share"** لتصدير الـ plan كـ file أو link

### الـ Sharing:

- **Offline file** — تصدير كـ JSON/Markdown
- **Private link** — لو بتشتغل مع team محلياً
- **Git-friendly** — تقدر تـ commit الـ plan في الـ repo

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ بتعمل **مهام كبيرة** محتاجة planning تفصيلي
- ✅ بتشتغل في **team** ومحتاج تشارك الـ plan قبل الـ implementation
- ✅ بتفضل الـ **visual review** بدل قراءة الـ plain text
- ✅ بتحب توثق قراراتك في كل خطوة
- ✅ بتعمل **مهام حساسة** في base-layer ومحتاج double-check
- ✅ بتشتغل على مشاريع **محتاج توثيق rationale** للقرارات
- ✅ شخصيتك **detail-oriented** (زي ما باين من شغلك)

### متستخدمهاش لو:
- ❌ بتعمل **tasks بسيطة** مش محتاجة planning
- ❌ بتفضل الـ **terminal-only workflow**
- ❌ بتشتغل **lone wolf** ومفيش team تشارك معاهم
- ❌ بتعمل **quick prototyping** ومستعجل
- ❌ بتستخدم **opencode-conductor** (في تداخل في الـ planning workflow)

---

## ⚠️ ملاحظات مهمة

### Browser Requirement:
محتاج browser محلي عشان تستخدم الـ UI.

### تعارض محتمل مع plugins تانية:
- **opencode-conductor** — برضه بيعمل planning، فممكن يكون فيه duplication
- **micode/octto** — برضه بيعمل planning workflow

في الحالات دي، اختار واحد بس عشان متاخدش double-planning prompts.

### الـ Privacy:
الـ data بتفضل محلية. الـ "private sharing" بيعتمد على:
- File export (JSON/Markdown)
- Local network sharing (لو بتشتغل في team محلي)

### Integration مع Git:
ممكن تـ commit الـ plans في `docs/plans/` أو `.opencode/plans/` للتوثيق.

```bash
git add docs/plans/jwt-refactor-plan.md
git commit -m "docs: add JWT refactor plan with annotations"
```

---

## 🔗 روابط مفيدة

- Repo: https://github.com/backnotprop/plannotator
- Plugin Path: https://github.com/backnotprop/plannotator/tree/main/apps/opencode-plugin
