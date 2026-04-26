# opencode-conductor-plugin

> النوع: Workflow / Process Plugin  
> الـ Repo: https://github.com/derekbar90/opencode-conductor  
> الـ NPM: `opencode-conductor-plugin`

---

## 1. إيه هي الإضافة دي؟

**Conductor** هي plugin بتفرض على الـ OpenCode منهجية شغل صارمة اسمها **Context-Driven Development**. الفلسفة بتاعتها بسيطة:

> **"Measure twice, code once"** — قس مرتين، اقطع مرة واحدة.

بدل ما الـ AI agent يكتب كود فوراً لما تطلب منه حاجة، الـ Conductor بيجبره يتبع protocol صارم:

```
Context → Spec → Plan → Implement
```

يعني:
1. الأول يفهم الـ context الكامل للمشروع
2. يكتب specification (مواصفات) واضحة
3. يعمل plan تفصيلي
4. وبعدين يبدأ يكتب كود

### المكونات:

- 🎭 **`@conductor` Agent** — agent متخصص يشتغل كـ "Project Architect" و "Technical Lead"
- ⚡ **Slash Commands** — `/conductor:setup`, `/conductor:newTrack`, `/conductor:implement`, إلخ
- 🔁 **Smart Revert** — نظام revert ذكي بيفهم الـ Git على مستوى Tracks/Phases/Tasks مش commits
- 📚 **19+ Style Templates** — Rust, Solidity, Zig, Julia, Kotlin, Swift، وغيرهم

---

## 2. في ماذا تستخدم؟

استخدمها لما تحب:

- ✅ **منع الـ AI من القفز على الـ implementation** قبل ما يفهم
- ✅ **توثيق المشروع تلقائياً** عبر spec.md و plan.md
- ✅ **تنظيم الشغل في "Tracks"** كل واحد ليه spec و plan
- ✅ **Semantic commits** تلقائي بعد كل task
- ✅ **Revert ذكي** على مستوى logical units (مش commit hashes)
- ✅ **Project Constitution** — قوانين المشروع موثقة (testing standards, commit strategy, إلخ)
- ✅ **Synergy مع Oh My OpenCode** — بيشتغلوا مع بعض كويس جداً

---

## 3. كيف تستخدم؟

### التثبيت

في `~/.config/opencode/opencode.json`:

```json
{
  "plugin": [
    "opencode-conductor-plugin"
  ]
}
```

> ⚠️ **مهم**: لازم تعمل restart للـ OpenCode بعد أول مرة عشان الـ slash commands تشتغل globally.

### إعدادات الموديل (موصى بيها)

`@conductor` بيشتغل أحسن مع موديل سريع زي Gemini Flash. أضف في الـ config:

```json
{
  "agent": {
    "conductor": {
      "model": "google/gemini-3-flash"
    }
  }
}
```

### مع Oh My OpenCode:

في `~/.config/opencode/oh-my-opencode.json`:

```json
{
  "agents": {
    "conductor": {
      "model": "google/gemini-3-flash"
    }
  }
}
```

### الـ Workflow الأساسي

#### 1️⃣ مرة واحدة بس لكل مشروع: `/conductor:setup`

```
/conductor:setup
```

الـ Conductor هيعمل interview معاك ويسألك عن:
- **Product Vision**: المستخدمين، الأهداف، المميزات
- **Tech Stack**: لغات، frameworks، databases
- **Workflow Rules**: testing standards (TDD/BDD)، commit strategy، documentation patterns

ده بيعمل ملف "Project Constitution".

#### 2️⃣ كل feature/bugfix جديد: `/conductor:newTrack`

```
/conductor:newTrack "Add dark mode toggle to settings page"
```

Conductor هيعمل:
- **`spec.md`** — يسألك 3-5 أسئلة محددة عشان يفهم الـ "What" و "Why"
- **`plan.md`** — قائمة step-by-step بالمهام طبقاً لقوانين المشروع

#### 3️⃣ التنفيذ: `/conductor:implement`

```
/conductor:implement
```

الـ Conductor هيشتغل على الـ `plan.md` ويعمل:
- ينفذ كل task
- يشغل الـ tests
- يعمل semantic commits تلقائياً
- مش هيقف لحد ما الـ Track يخلص

### الأوامر الكاملة

| الأمر | الوظيفة |
|------|---------|
| `/conductor:setup` | تهيئة المشروع + الـ Constitution |
| `/conductor:newTrack "desc"` | بدء Track جديد مع spec و plan |
| `/conductor:implement` | تنفيذ المهام الـ pending في الـ Track الحالي |
| `/conductor:status` | overview للـ project progress و الـ tracks |
| `/conductor:revert` | revert تفاعلي على مستوى task/phase/track |

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ بتشتغل على **مشاريع كبيرة** أو طويلة المدى
- ✅ محتاج **توثيق المشروع** تلقائياً (للـ team أو للنفس)
- ✅ بتحب الـ **structured workflows** (شخصيتك detail-oriented)
- ✅ بتعمل **مشاريع فيها ميزات كتيرة** ومحتاج تنظيم
- ✅ بتشتغل مع **team** ومحتاجين منهجية موحدة
- ✅ بتعمل **bug fixes معقدة** محتاجة planning قبل الكود
- ✅ بتاع base-layer architecture في Nanosoft — ده مناسب جداً لشغلك

### متستخدمهاش لو:
- ❌ بتعمل **scripts صغيرة** أو tasks سريعة
- ❌ بتعمل **prototyping سريع** ومش محتاج formality
- ❌ بتحب الـ **agile/iterative** workflow بدون planning مسبق
- ❌ مش عايز تكتب specs و plans لكل feature

---

## ⚠️ ملاحظات مهمة

### Loop Protection مع Oh My OpenCode:
الـ Conductor فيه built-in "Loop Protection" عشان مايتعارضش مع الـ continuation enforcers بتاع OmO أثناء الـ Q&A.

### Conductor ضد Oh My OpenCode:
- **Sisyphus** (في OmO) = الـ orchestrator العام والـ conversation
- **`@conductor`** (في الـ plugin ده) = Technical Lead للـ architecture و الـ planning

ممكن Sisyphus يـ delegate للـ `@conductor` لما يحتاج planning محكم.

### Agent Agnostic:
الـ Commands بتاعت Conductor ممكن تتاخد من أي agent تاني، مش بس `@conductor`. ده بيديك حرية اختيار الـ interface الأساسي.

### الـ Versioning:
بيتبع Conventional Commits + Semantic Release:
- `feat:` → minor version
- `fix:` → patch version
- `BREAKING CHANGE:` → major version

### الترخيص: Apache-2.0

---

## 🔗 روابط مفيدة

- README: https://github.com/derekbar90/opencode-conductor
- INSTALL.md: https://github.com/derekbar90/opencode-conductor/blob/main/INSTALL.md
- CHANGELOG: https://github.com/derekbar90/opencode-conductor/blob/main/CHANGELOG.md
