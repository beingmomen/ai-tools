# opencode-workspace

> النوع: Bundled Multi-Agent Harness (مجموعة متكاملة من الـ plugins)  
> الـ Repo: https://github.com/kdcokenny/opencode-workspace  
> الـ Stars: 340+ ⭐

---

## 1. إيه هي الإضافة دي؟

**opencode-workspace** هي **bundle متكامل** فيه 16 component بيشتغلوا مع بعض كـ نظام orchestration كامل للـ AI development.

تخيلها زي "package deal" — install واحد بيديك:
- 🔌 **6 plugins**
- 🧠 **3 MCP servers**
- 🤖 **4 agents**
- 🎨 **4 skills**
- 💬 **1 command**
- ⚙️ **Permission boundaries** و **agent sandboxing**

ده بديل لـ `oh-my-opencode` بس بفلسفة مختلفة:
- OmO → focused على الـ multi-model orchestration
- Workspace → focused على الـ structured roles مع OpenCode Free Models

---

## 2. في ماذا تستخدم؟

استخدمها لما تحب:

- ✅ **منظومة متكاملة جاهزة** بدون ما تركب كل plugin لوحده
- ✅ **OpenCode Free Models support** (الـ profile الافتراضي)
- ✅ **Architecture منظمة** بـ Orchestrators (`plan`, `build`) و Specialists
- ✅ **Permissions مضبوطة** افتراضياً (security-first)
- ✅ **MCPs جاهزة**: Context7 (docs)، Exa (search)، GitHub Grep
- ✅ **OCX integration** — package manager خاص بهم للـ updates السهلة
- ✅ **Profiles قابلة للتخصيص** — تقدر تعدل وتعمل profile بتاعك

### الـ Components كاملة:

| Category | Component | الوظيفة |
|----------|-----------|---------|
| Plugin | `workspace-plugin` | إدارة الـ plans + agent rule injection |
| Plugin | `background-agents` | نظام delegation async |
| Plugin | `notify` | OS notifications عند الـ completion |
| Plugin | `worktree` | Git worktree isolation |
| Plugin | `@tarquinen/opencode-dcp` | Differential Context Pruning |
| Plugin | `@franlol/opencode-md-table-formatter` | تنسيق الـ markdown tables |
| Skill | `plan-protocol` | Implementation planning guidelines |
| Skill | `code-review` | Code review methodology |
| Skill | `code-philosophy` | Internal logic philosophy (5 Laws) |
| Skill | `frontend-philosophy` | Visual/UI philosophy (5 Pillars) |
| Agent | `researcher` | External research (read-only + MCP) |
| Agent | `coder` | Implementation (full file + bash) |
| Agent | `scribe` | Documentation (write only) |
| Agent | `reviewer` | Code review (read-only + git) |
| Command | `review` | `/review` slash command |
| MCP | `context7` | البحث في docs المكتبات |
| MCP | `exa` | Web search للـ research |
| MCP | `gh_grep` | البحث في GitHub code |

### Architecture:

```
┌─────────────────────────────────────────────────┐
│              ORCHESTRATORS                      │
│         ┌─────┐         ┌─────┐                │
│         │plan │         │build│                │
│         └──┬──┘         └──┬──┘                │
└────────────┼───────────────┼────────────────────┘
             │               │
     ┌───────┴───────┐   ┌───┴───┐
     ▼       ▼       ▼   ▼      ▼      ▼
┌───────┐ ┌────────┐ ┌─────┐ ┌─────┐ ┌──────┐
│explore│ │research│ │coder│ │scribe│ │review│
└───────┘ └────────┘ └─────┘ └─────┘ └──────┘
                  SPECIALISTS
```

---

## 3. كيف تستخدم؟

### الخطوة 1: تثبيت OCX

OCX هو الـ package manager الخاص بهم. لو مش متركب:

```bash
# من الـ OCX repo
# https://github.com/kdcokenny/ocx
```

### الخطوة 2: تثبيت الـ Workspace

```bash
# إعداد لمرة واحدة
ocx init --global

# تثبيت الـ KDCO workspace profile (OpenCode Free Models Only)
ocx profile add ws --source tweak/p-1vp4xoqv --from https://tweakoc.com/r --global

# Launch
ocx oc -p ws
```

### الطريقة البديلة (Direct Install بدون profile):

```bash
ocx add kdco/workspace --from https://registry.kdco.dev
```

### Profile مخصص:

تقدر تفتح الـ harness في TweakOC وتخصصه:  
https://tweakoc.com/h/kdco-workspace

### الـ Permissions الافتراضية:

| Scope | الإعداد |
|-------|---------|
| Global | `webfetch: deny` — مفيش web fetching مباشر |
| `plan` | Read-only orchestrator، delegates عبر `task` |
| `build` | Read-only orchestrator، delegates عبر `task` |
| `explore` | Read-only specialist، filesystem + git فقط |
| `researcher` | Read-only، MCP tools فقط |
| `coder` | Full file + bash access |
| `scribe` | File write only، **مفيش bash** |
| `reviewer` | Read-only + git inspection |

### الاستخدام اليومي

```bash
# تشغيل OpenCode بالـ workspace profile
ocx oc -p ws

# استخدم الأوامر العادية في OpenCode
# /review - لمراجعة كود
# الـ orchestrators (plan, build) بيستخدموا الـ specialists تلقائي
```

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ عايز **حل متكامل** بدون ما تركب كل plugin لوحده
- ✅ بتفضل الـ **OpenCode Free Models** (Gemini Free)
- ✅ محتاج **architecture منظمة** بـ roles واضحة (planner, coder, reviewer)
- ✅ بتشتغل على **مشاريع متعددة** ومحتاج permissions مضبوطة
- ✅ مهتم بالـ **security** (الـ permissions defaults مدققة)
- ✅ عايز **MCPs جاهزة** (Context7, Exa, GitHub Grep)
- ✅ بتحب نظام الـ **OCX profiles** للتنقل بين environments

### متستخدمهاش لو:
- ❌ مش حابب الاعتماد على **OCX package manager**
- ❌ عايز **تحكم granular** في كل plugin منفصل
- ❌ بتستخدم **oh-my-opencode** بالفعل (تداخل في الـ agents)
- ❌ بتشتغل بـ **paid models** ومش محتاج الـ free profile

---

## ⚠️ ملاحظات مهمة

### Workspace ضد Oh My OpenCode:

| الجانب | OmO | Workspace |
|--------|-----|-----------|
| الفلسفة | Multi-model orchestration | Structured role-based |
| الموديلات | Claude/Kimi/GPT/Gemini | OpenCode Free Models |
| الـ Agents | Sisyphus, Hephaestus, إلخ | plan, build, coder, scribe |
| Package Manager | npm | OCX |
| Permissions | Flexible | Strict by default |

### الـ Repository Structure:
- الـ facade بيتم maintain من main OCX monorepo
- لازم تفتح issues في الـ OCX monorepo، **مش في الـ facade repo**
- https://github.com/kdcokenny/ocx

### Owning Your Code:
كل ملف في الـ bundle synced بالـ repo. ممكن تـ:
- Fork الـ repo
- تعدل الـ agents
- تضبط الـ skills
- تخصصها لشغلك

### Disclaimer:
المشروع ده **مش رسمي** من فريق OpenCode، وغير مرتبط بـ [SST OpenCode](https://github.com/sst/opencode) بأي شكل.

### الترخيص: MIT

---

## 🔗 روابط مفيدة

- README: https://github.com/kdcokenny/opencode-workspace
- OCX Repo: https://github.com/kdcokenny/ocx
- TweakOC: https://tweakoc.com/h/kdco-workspace
- Installation Guide: https://github.com/kdcokenny/opencode-workspace/docs/guides/kdco-workspace.mdx
