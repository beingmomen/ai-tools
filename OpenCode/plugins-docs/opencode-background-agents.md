# opencode-background-agents

> النوع: Async Agent Delegation Plugin  
> الـ Repo: https://github.com/kdcokenny/opencode-background-agents

---

## 1. إيه هي الإضافة دي؟

**opencode-background-agents** هي plugin بيدي الـ OpenCode قدرة الـ **Background Agents** على نمط Claude Code. الفكرة الأساسية:

- بدل ما الـ agent يشتغل على المهمة بشكل blocking ويـ block الـ session بتاعتك
- بيشغل **agents في الخلفية** بشكل async مع context منفصل
- بيرجعلك **لما يخلصوا** بدون ما يقطعوا شغلك

تخيلها كأنك بتشغل team من الـ junior developers بشكل متوازي، وكل واحد بيشتغل على مهمة لوحده.

### الفرق بين Background Agents والـ Subagents العادية:

| الجانب | Subagents العادي | Background Agents |
|--------|------------------|-------------------|
| التشغيل | Sequential (متتابع) | Parallel (متوازي) |
| الـ Context | بيشارك مع الـ main agent | منفصل تماماً |
| الـ Blocking | بيـ block الـ session | Async (مش بيـ block) |
| الاستخدام | tasks بسيطة | tasks طويلة ومعقدة |

---

## 2. في ماذا تستخدم؟

استخدمها عشان:

- ✅ **تشغيل 5+ agents متوازي** كل واحد بمهمة مختلفة
- ✅ **Context Persistence** — كل agent ليه context منفصل ومش بيتلوث
- ✅ **Async Delegation** — بتديهم المهمة وترجع تشتغل في حاجة تانية
- ✅ **Notifications** لما المهمة تخلص
- ✅ **Lean Main Context** — الـ session الرئيسي بتاعك بيفضل خفيف
- ✅ **توازي حقيقي** — متعمل في عشر دقائق اللي كان هياخد ساعة

### السيناريو النموذجي:

```
أنت: "Refactor the auth system, write tests for it, 
       and update the docs"

Background Agents:
- Agent 1 → بيـ refactor الـ auth (background)
- Agent 2 → بيكتب tests (background)  
- Agent 3 → بيـ update docs (background)
- الـ Main Session → فاضي تشتغل على حاجة تانية

[بعد 10 دقايق]
🔔 Agent 1 finished: Auth refactored
🔔 Agent 2 finished: 15 tests added
🔔 Agent 3 finished: Docs updated
```

---

## 3. كيف تستخدم؟

### التثبيت

في `~/.config/opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["opencode-background-agents"]
}
```

### التشغيل

الـ plugin بيضيف tools و commands جديدة للـ OpenCode عشان تـ:

1. **تطلق agent في الـ background**:
   ```
   اطلق agent في الـ background يعمل refactor للـ auth module
   ```

2. **تتابع status الـ agents**:
   ```
   status agents
   ```

3. **تجيب نتائج agent خلص**:
   ```
   get results from agent <id>
   ```

### مع Plugins تانية

الـ plugin ده part من الـ **opencode-workspace** bundle، فلو بتستخدم workspace، الـ plugin ده موجود بالفعل.

كمان متوافق مع:
- ✅ **oh-my-opencode** — OmO عنده Background Agents بالفعل، فممكن يكون فيه تداخل
- ✅ **opencode-notify** — لتلقي notifications لما الـ agents يخلصوا
- ✅ **opencode-supermemory** — كل agent ليه access للـ memory

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ بتشتغل على **مهام كبيرة** ممكن تتقسم لـ subtasks مستقلة
- ✅ محتاج **توازي حقيقي** بدل sequential execution
- ✅ بتعمل **refactoring كبير** + tests + docs في نفس الوقت
- ✅ بتشتغل على **monorepo** فيه أكتر من package
- ✅ شغلك على **base-layer** فيه multiple modules مستقلة عن بعض
- ✅ بتفضل الـ **non-blocking workflow**

### متستخدمهاش لو:
- ❌ بتعمل **tasks تتابعية** (الخطوة الثانية محتاجة الأولى)
- ❌ بتشتغل على **حاجة بسيطة** ومش محتاج توازي
- ❌ بتستخدم **oh-my-opencode** (عنده background agents بالفعل)
- ❌ في **API rate limits** قاسية (التوازي هيستهلكها بسرعة)
- ❌ بتشتغل بـ **free models** ذات quota محدود

---

## ⚠️ ملاحظات مهمة

### الـ API Cost:
كل background agent بيستهلك tokens مستقلة. لو شغلت 5 agents متوازي، التكلفة بتـ x5 تقريباً.

### Model Selection:
لازم تضبط الموديل المناسب لكل agent على حسب طبيعة المهمة. بعض المهام محتاجة Opus والتانية تكفي معاها Haiku.

### Subagent Notifications:
لو بتستخدم `opencode-notifier`، الـ subagent_complete event بيكون silent بشكل افتراضي (عشان متاخدش spam لما 5 agents يخلصوا في نفس الوقت). تقدر تفعله من الـ config.

### تعارض محتمل مع Oh My OpenCode:
لو بتستخدم OmO، هي بالفعل عندها نظام Background Agents الخاص بيها (Sisyphus بيـ delegate لـ Hephaestus، Oracle، Librarian). فممكن يحصل تداخل أو duplication.

---

## 🔗 روابط مفيدة

- Repo: https://github.com/kdcokenny/opencode-background-agents
- Bundle (workspace): https://github.com/kdcokenny/opencode-workspace
