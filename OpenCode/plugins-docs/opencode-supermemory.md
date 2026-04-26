# opencode-supermemory

> النوع: Persistent Memory Plugin  
> الـ Repo: https://github.com/supermemoryai/opencode-supermemory  
> الموقع الرسمي: https://supermemory.ai  
> الـ Stars: 908+ ⭐

---

## 1. إيه هي الإضافة دي؟

**opencode-supermemory** هي plugin بتدي الـ AI agent **ذاكرة دائمة** عبر الـ sessions والمشاريع. يعني الـ agent بيفتكر اللي اتفقتم عليه، اللي اتعلموه من الـ codebase بتاعك، وتفضيلاتك الشخصية.

تخيلها كـ "long-term memory" للـ AI:
- **بدون الـ plugin**: كل session جديدة، الـ AI نسي كل حاجة
- **مع الـ plugin**: الـ AI بيرجع للـ context القديم تلقائياً

### مستويات الذاكرة:

1. **User Profile** (cross-project) — تفضيلاتك الشخصية، أسلوبك في الكتابة، الموديلات اللي بتفضلها
2. **Project Memories** — معلومات خاصة بالمشروع (zo`uses Bun not Node.js`، `build commands`، إلخ)
3. **Session Summaries** — ملخصات للـ sessions السابقة

---

## 2. في ماذا تستخدم؟

استخدمها عشان:

- ✅ **الـ agent يفتكر** اللي اتعلمه من قبل
- ✅ **Codebase Indexing** — الـ agent بيستكشف الـ codebase بتاعك ويحفظ patterns و conventions
- ✅ **Auto-Save** بكلمات زي "remember"، "save this"، "don't forget"
- ✅ **Context Injection** — في أول رسالة، الـ agent بيستلم context كامل من الذاكرة
- ✅ **Preemptive Compaction** — لما الـ context يوصل 80%، بيـ compact قبل ما يضيع المعلومات
- ✅ **Privacy Tags** — `<private>data</private>` مش بيتحفظ
- ✅ **Cross-Project User Profile** — تفضيلاتك بتنتقل بين كل مشاريعك

### مثال على الـ Context اللي الـ agent بيشوفه:

```
[SUPERMEMORY]

User Profile:
- Prefers concise responses
- Expert in TypeScript

Project Knowledge:
- [100%] Uses Bun, not Node.js
- [100%] Build: bun run build

Relevant Memories:
- [82%] Build fails if .env.local missing
```

---

## 3. كيف تستخدم؟

### الخطوة 1: التثبيت

```bash
bunx opencode-supermemory@latest install
```

ده هيضيف الـ plugin تلقائياً في `~/.config/opencode/opencode.jsonc` ويعمل الـ `/supermemory-init` command.

### الخطوة 2: الحصول على API Key

روح لـ [app.supermemory.ai](https://app.supermemory.ai/?view=integrations) واعمل حساب وخد الـ API key.

### الخطوة 3: ضبط الـ API Key

عبر environment variable:

```bash
export SUPERMEMORY_API_KEY="sm_..."
```

أو في ملف `~/.config/opencode/supermemory.jsonc`:

```jsonc
{
  "apiKey": "sm_...",
  
  "similarityThreshold": 0.6,    // الحد الأدنى للـ similarity في البحث
  "maxMemories": 5,              // أقصى عدد ذكريات بتنحقن في الـ request
  "maxProjectMemories": 10,      // أقصى عدد project memories
  "maxProfileItems": 5,          // أقصى profile facts
  "injectProfile": true,         // ضمن الـ user profile في الـ context
  "compactionThreshold": 0.8     // نسبة الاستهلاك اللي تطلق الـ compaction
}
```

### الخطوة 4: تهيئة الـ Codebase (اختياري لكن موصى به)

```
/supermemory-init
```

ده بيخلي الـ agent يستكشف الـ codebase ويحفظ:
- بنية المشروع
- الـ patterns المستخدمة
- الـ conventions الخاصة بالكود

### الاستخدام اليومي

#### الحفظ التلقائي (Keyword Detection):

```
أنت: "Remember that this project uses bun"
الـ Agent: [يحفظ في project memory تلقائياً]

أنت: "don't forget that we use Pinia for state management"
الـ Agent: [يحفظ تلقائياً]
```

#### الأداة `supermemory` متاحة للـ agent بـ 5 modes:

| Mode | الوظيفة |
|------|---------|
| `add` | حفظ ذكرى جديدة |
| `search` | البحث في الذكريات |
| `profile` | عرض الـ user profile |
| `list` | قائمة بالذكريات |
| `forget` | حذف ذكرى معينة |

#### الـ Scopes:

- **`user`** — cross-project (تفضيلات شخصية، تنتقل بين المشاريع)
- **`project`** (default) — خاصة بالمشروع الحالي

#### الـ Types:

- `project-config`
- `architecture`
- `error-solution`
- `preference`
- `learned-pattern`
- `conversation`

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ بتشتغل على نفس الـ codebase **لفترات طويلة** (زي base-layer بتاعك في Nanosoft)
- ✅ عندك **معلومات متكررة** بتقولها للـ AI كل مرة
- ✅ بتعمل **مشاريع متعددة** ومحتاج الـ agent يفتكر تفضيلاتك
- ✅ بتحب الـ **continuity** بين الـ sessions
- ✅ بتعمل **bug fixes متكررة** ومحتاج الـ agent يفتكر الحلول
- ✅ شغلك **detail-oriented** زي شخصيتك

### متستخدمهاش لو:
- ❌ بتعمل **prototyping سريع** على مشاريع متغيرة
- ❌ بتشتغل على مشاريع **حساسة الخصوصية** (الـ data بيروح لخوادم Supermemory)
- ❌ مش حابب **dependency خارجية** على service
- ❌ شغلك **ذو طبيعة مختلفة كل مرة** ومفيش continuity

---

## ⚠️ ملاحظات مهمة

### مع Oh My OpenCode:
لو بتستخدم OmO، لازم تعطل الـ auto-compact hook عشان supermemory تعمل الـ compaction:

في `~/.config/opencode/oh-my-opencode.json`:

```json
{
  "disabled_hooks": ["anthropic-context-window-limit-recovery"]
}
```

### الـ Container Tags:
الـ tags بتولد تلقائياً:
- User: `opencode_user_{sha256(git_email)}`
- Project: `opencode_project_{sha256(directory)}`

ممكن تخصصها لو:
- **مشاركة ذكريات** بين أعضاء الفريق (نفس الـ `userContainerTag`)
- **مزامنة** بين أجهزة مختلفة
- **تنظيم** الذكريات بطريقتك

```jsonc
{
  "userContainerTag": "my-team-workspace",
  "projectContainerTag": "nanosoft-base-layer"
}
```

### Privacy:
أي حاجة جوه `<private>...</private>` tags **مش بيتحفظ**. مفيد للـ API keys والـ secrets.

```
API key is <private>sk-abc123</private>
```

### Logs:
```bash
tail -f ~/.opencode-supermemory.log
```

### الترخيص: MIT

---

## 🔗 روابط مفيدة

- README: https://github.com/supermemoryai/opencode-supermemory
- Supermemory App: https://app.supermemory.ai
- Documentation: https://supermemory.ai/docs/integrations/opencode
