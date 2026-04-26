# 🎯 OpenCode Plugins — الإعدادات الجاهزة للمشاريع

> دليل سريع لاختيار الـ plugins المناسبة لكل نوع مشروع  
> **كل الإعدادات مجانية 100%** ومضبوطة على **Project Scope**

---

## 📑 الفهرس السريع

اختار الـ Preset اللي يناسب مشروعك من الجدول، وانسخ الإعداد مباشرة:

| # | الـ Preset | استخدمه لما... |
|---|-----------|----------------|
| 1️⃣ | [مشروع كبير ومتكامل من الصفر](#1️⃣-preset-1--مشروع-كبير-ومتكامل-من-الصفر) | بتبني product/app كامل من البداية، وهتشتغل عليه أسابيع/شهور |
| 2️⃣ | [Task سريع أو Bug Fix بسيط](#2️⃣-preset-2--task-سريع-أو-bug-fix-بسيط) | عندك تعديل بسيط، script صغير، أو bug محتاج حل سريع |
| 3️⃣ | [Refactoring لمشروع موجود](#3️⃣-preset-3--refactoring-لمشروع-موجود) | بتعدّل في codebase موجود، تعمل migration، أو cleanup كبير |
| 4️⃣ | [استكشاف Codebase جديد](#4️⃣-preset-4--استكشاف-codebase-جديد) | لسه داخل على project مش متعرف عليه، عايز تفهمه قبل ما تبدأ |
| 5️⃣ | [شغل منظم بـ Specs و Plans](#5️⃣-preset-5--شغل-منظم-بـ-specs-و-plans) | محتاج توثيق رسمي للـ features، شغل team، أو شغل عميل |

---

## 🚀 طريقة الاستخدام

كل preset عبارة عن ملف `opencode.json` بيتحط في **root المشروع** (مش global).

```
your-project/
├── opencode.json    ← هنا
├── package.json
├── src/
└── ...
```

**خطوة لمرة واحدة فقط (للجهاز كله):**

```bash
opencode auth login
# اختار: Google → OAuth with Google (Antigravity)
```

بعدها كل projects بتاعتك هتقدر تستخدم Gemini 3 Pro و Claude Opus/Sonnet **مجاناً**.

---

## 1️⃣ Preset #1 — مشروع كبير ومتكامل من الصفر

### 📌 امتى تستخدم؟

- بتبدأ **product/app كامل** من الصفر
- المشروع هياخد منك **أسابيع أو شهور**
- محتاج كل المميزات: orchestration + multi-agents + edit tools دقيقة + context management + notifications
- أمثلة:
  - SaaS dashboard من الصفر
  - API كامل بـ authentication و database
  - Mobile app بـ multiple screens
  - Nuxt 4 application كاملة

### 🎁 إيه اللي بتاخده؟

- **`oh-my-opencode` (OmO)**: harness شامل بيوفر:
  - فريق agents بيشتغلوا متوازي (Sisyphus orchestrator + Hephaestus worker + Prometheus planner)
  - Background Agents (5+ agents بشكل async)
  - Hash-Anchored Edit Tool (تعديلات دقيقة بدون stale-line errors)
  - Context management ذكي
  - Notifications hooks مدمجة
  - MCPs جاهزة (Exa search, Context7 docs, Grep.app)
  - أمر `ulw` (ultrawork) — كلمة واحدة بتشغّل كل المنظومة
- **`opencode-google-antigravity-auth`**: Gemini 3 Pro + Claude مجاناً

### 📄 الإعداد

**`<project-root>/opencode.json`:**

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "oh-my-opencode",
    "opencode-google-antigravity-auth"
  ]
}
```

### 💻 الاستخدام اليومي

```bash
# جوه OpenCode، بدل أوامر معقدة، اكتب:
ulw build a dashboard with auth and dark mode
```

---

## 2️⃣ Preset #2 — Task سريع أو Bug Fix بسيط

### 📌 امتى تستخدم؟

- **شغل ساعة أو ساعتين** بحد أقصى
- bug fix محدد
- script أو utility صغير
- تعديل في component موجود
- مش محتاج orchestration معقد ولا multi-agents
- أمثلة:
  - "اعملي validation لل form ده"
  - "صلح الـ error في الـ login"
  - "اعملي helper function للـ date formatting"
  - "ضيف dark mode toggle"

### 🎁 إيه اللي بتاخده؟

- **`opencode-google-antigravity-auth`**: Gemini 3 Pro مجاناً
- **`@tarquinen/opencode-dcp`**: توفير tokens بشكل ذكي (deduplication + error pruning)
- **`@mohak34/opencode-notifier`**: تنبيهات لما الـ task يخلص أو يحتاج إذن

### 📄 الإعداد

**`<project-root>/opencode.json`:**

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "opencode-google-antigravity-auth",
    "@tarquinen/opencode-dcp@latest",
    "@mohak34/opencode-notifier@latest"
  ]
}
```

### 💻 الاستخدام اليومي

```bash
# عادي، بدون أوامر خاصة
opencode
```

---

## 3️⃣ Preset #3 — Refactoring لمشروع موجود

### 📌 امتى تستخدم؟

- بتعدل في **codebase موجود**
- بتعمل **migration** من تكنولوجيا لتانية
- بتعمل **cleanup** لكود قديم
- بتعمل **code reorganization** كبير
- أمثلة:
  - تحويل من Options API لـ Composition API في Vue
  - migration من JavaScript لـ TypeScript
  - فصل monolith لـ modules
  - تحديث base-layer architecture
  - استبدال state management library

### 🎁 إيه اللي بتاخده؟

- **`oh-my-opencode` (OmO)**: مهم جداً للـ refactoring لأنه بيوفر:
  - **Hash-Anchored Edit Tool**: كل سطر بياخد content hash، فلو الفايل اتغير، التعديل بيترفض قبل ما يبوظ الكود (Grok Code Fast حقق نسبة نجاح من 6.7% لـ 68.3% بسبب الأداة دي)
  - **AST-Grep**: تعديلات بـ pattern matching على مستوى الـ AST بـ 25 لغة
  - **LSP integration**: rename، find references، goto definition
  - **Background Agents**: تعمل refactoring متوازي على modules مختلفة
- **`opencode-google-antigravity-auth`**: Gemini 3 Pro مجاناً

### 📄 الإعداد

**`<project-root>/opencode.json`:**

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "oh-my-opencode",
    "opencode-google-antigravity-auth"
  ]
}
```

### 💻 الاستخدام اليومي

```bash
ulw refactor the auth module to use composition API
```

---

## 4️⃣ Preset #4 — استكشاف Codebase جديد

### 📌 امتى تستخدم؟

- **داخل على مشروع لأول مرة** (شغل جديد، open-source contribution)
- محتاج **تفهم الـ architecture** قبل ما تبدأ تعدل
- مشروع **مش موثق كويس** ومحتاج توليد docs منه
- بتعمل **code review** عميق لـ codebase قديم
- أمثلة:
  - شغل جديد، استلمت codebase
  - معاد على feature معقد ومحتاج تفهم الـ flow
  - بتساهم في open-source project
  - وراثة مشروع من developer سابق

### 🎁 إيه اللي بتاخده؟

- **`oh-my-opencode` (OmO)** — أمر مهم جداً لده: **`/init-deep`**
  - بيستكشف الـ codebase تلقائياً
  - بيولّد ملفات `AGENTS.md` هرمية في كل مجلد
  - الـ AI بيستخدم الملفات دي كـ reference دائم
  - يعني الـ codebase بيبقى "موثق ذاتياً" بعد أول مرة
- **Librarian agent** و **Explore agent**: متخصصين في فهم الـ codebase
- **Built-in MCPs**: Context7 (docs المكتبات) + Grep.app (GitHub search)
- **`opencode-google-antigravity-auth`**: Gemini 3 Pro (1M context window — مفيد جداً للملفات الكبيرة)

### 📄 الإعداد

**`<project-root>/opencode.json`:**

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "oh-my-opencode",
    "opencode-google-antigravity-auth"
  ]
}
```

### 💻 الاستخدام اليومي

```bash
# أول حاجة تعملها في المشروع الجديد:
opencode

# جوه OpenCode، نفذ الأمر ده:
/init-deep

# بعد ما يخلص، شغّل:
ulw explain the architecture and main flows
```

---

## 5️⃣ Preset #5 — شغل منظم بـ Specs و Plans

### 📌 امتى تستخدم؟

- بتشتغل مع **team** ومحتاجين توثيق موحد
- بتشتغل لـ **عميل** ومحتاج specs قبل التنفيذ
- بتعمل **مهام حساسة** محتاجة planning قبل الكود
- بتحب الـ **structured workflow** (Specify → Plan → Implement)
- محتاج **revert ذكي** على مستوى features مش commits
- أمثلة:
  - features في product enterprise
  - عمل tickets جاهزة من الـ AI
  - شغل freelance بـ deliverables واضحة
  - مشاريع محتاجة audit trail

### 🎁 إيه اللي بتاخده؟

- **`opencode-conductor-plugin`**: بيفرض workflow صارم:
  - `/conductor:setup` — مرة واحدة لكل مشروع، بيعمل "Project Constitution"
  - `/conductor:newTrack "..."` — يبدأ feature جديدة بـ `spec.md` و `plan.md`
  - `/conductor:implement` — بينفذ الـ plan تلقائي مع semantic commits
  - `/conductor:revert` — revert ذكي على مستوى Tasks/Phases/Tracks
- **`@tarquinen/opencode-dcp`**: توفير tokens (مهم لأن الـ planning بيستهلك context)
- **`@mohak34/opencode-notifier`**: تنبيهات للـ permissions و completion
- **`opencode-google-antigravity-auth`**: Gemini 3 Flash للـ Conductor (سريع ورخيص للـ planning)

### 📄 الإعداد

**`<project-root>/opencode.json`:**

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "opencode-google-antigravity-auth",
    "opencode-conductor-plugin",
    "@tarquinen/opencode-dcp@latest",
    "@mohak34/opencode-notifier@latest"
  ],
  "agent": {
    "conductor": {
      "model": "google/gemini-3-flash"
    }
  }
}
```

### 💻 الاستخدام اليومي

```bash
# مرة واحدة لكل مشروع جديد:
/conductor:setup

# لكل feature أو bug:
/conductor:newTrack "Add JWT authentication to API"
# هيسألك 3-5 أسئلة، بعدها يولّد spec.md و plan.md

# لما الـ plan يبقى جاهز:
/conductor:implement

# لو محتاج تشوف الـ progress:
/conductor:status

# لو حصلت مشكلة وعايز ترجع:
/conductor:revert
```

---

## 📊 جدول مقارنة سريع

| الـ Plugin | Preset 1 | Preset 2 | Preset 3 | Preset 4 | Preset 5 |
|-----------|:--------:|:--------:|:--------:|:--------:|:--------:|
| `opencode-google-antigravity-auth` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `oh-my-opencode` | ✅ | ❌ | ✅ | ✅ | ❌ |
| `@tarquinen/opencode-dcp` | ❌ | ✅ | ❌ | ❌ | ✅ |
| `@mohak34/opencode-notifier` | ❌ | ✅ | ❌ | ❌ | ✅ |
| `opencode-conductor-plugin` | ❌ | ❌ | ❌ | ❌ | ✅ |

> **ملاحظة**: في Presets 1, 3, 4 الـ DCP و Notifier مش محتاجين لأن `oh-my-opencode` فيه بدائل مدمجة بنفس الكفاءة، وإضافتهم هتسبب تعارض.

---

## ⚠️ تنبيهات مهمة

### 🔴 الإضافات المدفوعة اللي تم استبعادها

| Plugin | السبب | البديل المجاني |
|--------|-------|----------------|
| `opencode-supermemory` | مدفوع بعد 100k tokens ($20/شهر) | استخدم `/init-deep` من OmO |
| `opencode-morph-fast-apply` | مدفوع بعد $2.50 credits | استخدم Hash-Anchored Edit من OmO |

### 🔴 الإضافات اللي بتعمل تعارض ومتجمعش بين بعض

- ❌ **متجمعش 3 auth plugins** مع بعض:
  - `opencode-google-antigravity-auth`
  - `opencode-antigravity-auth`
  - `opencode-gemini-auth`
  
  استخدم **واحد بس** (الأول هو الموصى به).

- ❌ **متجمعش `oh-my-opencode` مع `opencode-workspace`** — الاتنين harnesses شاملة وفيها duplication.

- ❌ **متجمعش `@tarquinen/opencode-dcp` مع `oh-my-opencode`** — OmO عنده context management بنفسه، وممكن يحصل تعارض في الـ compaction logic.

- ❌ **متجمعش `@mohak34/opencode-notifier` مع `oh-my-opencode`** — OmO عنده notification hooks بنفسه.

- ❌ **متجمعش `opencode-conductor-plugin` مع `@plannotator/opencode`** — الاتنين بيعملوا planning workflows متضاربة.

### 🟡 تنبيهات على Antigravity Auth

- في **تقارير عن حظر حسابات Google** اللي بتستخدم الـ plugin.
- استخدم **حساب Google ثانوي** مش الأساسي.
- الـ repo اتأرشف في فبراير 2026 بس الـ plugin لسه شغال.

---

## 🛠️ Troubleshooting

### الـ Plugin مش بيتحدث

```bash
# Linux/macOS
rm -rf ~/.cache/opencode/node_modules/<plugin-name>

# Windows
Remove-Item -Recurse -Force "$env:USERPROFILE\.cache\opencode\node_modules\<plugin-name>"
```

ثم restart الـ OpenCode.

### مشكلة في Antigravity Auth

```bash
# سجل دخول من جديد
opencode auth login

# Debug
opencode --log-level DEBUG --print-logs
```

### الـ Conductor مش شغال

تأكد إنك عملت restart للـ OpenCode بعد أول تثبيت — لازم عشان الـ slash commands يشتغلوا.

---

## 🎯 توصيتي الشخصية

لو لسه متحير، ابدأ كده:

1. **مشروع جديد كبير؟** → استخدم **Preset #1**
2. **شغل يومي عادي؟** → استخدم **Preset #2**  
3. **مش متأكد؟** → ابدأ بـ **Preset #2**، ولو حسيت إن المشروع بيكبر، انقل لـ **Preset #1** أو **#5**

---

## 🔗 روابط مفيدة

- OpenCode Docs: https://opencode.ai/docs/
- Plugins Documentation: https://opencode.ai/docs/plugins/
- Ecosystem: https://opencode.ai/docs/ecosystem
- oh-my-opencode: https://github.com/code-yeongyu/oh-my-opencode
- Antigravity Auth: https://github.com/shekohex/opencode-google-antigravity-auth
- DCP: https://github.com/Opencode-DCP/opencode-dynamic-context-pruning
- Notifier: https://github.com/mohak34/opencode-notifier
- Conductor: https://github.com/derekbar90/opencode-conductor
