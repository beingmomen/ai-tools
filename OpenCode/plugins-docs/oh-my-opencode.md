# oh-my-opencode

> النوع: Agent Harness شامل (الأكثر شمولاً في القائمة)  
> الـ Repo: https://github.com/code-yeongyu/oh-my-opencode  
> الـ Stars: 37.4k+ ⭐

---

## 1. إيه هي الإضافة دي؟

**oh-my-opencode** (اختصاراً: OmO) هو "agent harness" متكامل، يعني مش مجرد plugin عادي - ده package كامل بيحول الـ OpenCode من أداة بسيطة لـ **منظومة شغل احترافية كاملة** فيها فريق من الـ AI agents بيشتغلوا متوازي.

الـ plugin متبني على فلسفة إن مفيش موديل واحد بيبقى الأفضل في كل حاجة، فبيستخدم موديلات مختلفة لمهام مختلفة (Claude Opus، Kimi K2.5، GPT-5.3 Codex، Gemini)، وكل agent متخصص في حاجة معينة.

### الـ Agents اللي بيوفرها:
- **Sisyphus** (الـ orchestrator الرئيسي) — بيخطط، يوزع المهام، ومش بيقف لحد ما يخلص الشغل.
- **Hephaestus** (الـ deep worker) — بيشتغل لوحده على مهام كبيرة من غير ما تشرحله كل خطوة.
- **Prometheus** (الـ planner) — بيعمل interview معاك ويعمل خطة قبل ما يكتب أي كود.
- **Oracle، Librarian، Explore** — متخصصين في architecture، docs، والبحث في الـ codebase.

---

## 2. في ماذا تستخدم؟

استخدمها لما تحب تحول الـ OpenCode لتجربة كاملة قريبة من Claude Code أو Cursor، مع المميزات دي:

- ✅ **Background Agents** — تشغيل 5+ agents متوازي مع context منفصل لكل واحد
- ✅ **LSP + AST-Grep tools** — refactoring و rename بدقة الـ IDE
- ✅ **Hash-Anchored Edit Tool** — تعديلات دقيقة من غير "stale-line errors"
- ✅ **MCPs مدمجة جاهزة**: Exa (web search)، Context7 (docs)، Grep.app (GitHub search)
- ✅ **Ralph Loop** (`/ulw-loop`) — loop ذاتي مش بيقف لحد ما المهمة تخلص 100%
- ✅ **Tmux Integration** — terminal تفاعلي كامل (REPLs، debuggers، TUIs)
- ✅ **Skill-Embedded MCPs** — skills بتجي معاها MCP servers خاصة
- ✅ **متوافق مع Claude Code** — hooks، commands، skills، MCPs، plugins كلها بتشتغل
- ✅ **`/init-deep`** — توليد ملفات `AGENTS.md` هرمياً لكل مجلد

---

## 3. كيف تستخدم؟

### التثبيت (الطريقة الموصى بها)

افتح أي AI agent عندك (Claude Code, Cursor, إلخ) وقوله:

```
Install and configure oh-my-opencode by following the instructions here:
https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/refs/heads/dev/docs/guide/installation.md
```

أو بدوياً عن طريق إضافته في `~/.config/opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["oh-my-opencode"]
}
```

### الاستخدام اليومي

كلمة واحدة بس: **`ultrawork`** (أو اختصاراً `ulw`).

```
ulw build a Nuxt 4 dashboard with auth and dark mode
```

كل الـ agents هتشتغل متوازية، والـ system هيختار الموديل المناسب لكل مهمة لوحده.

### إعدادات إضافية

- ملفات الإعداد: `.opencode/oh-my-opencode.jsonc` (للمشروع) أو `~/.config/opencode/oh-my-opencode.jsonc` (عام)
- بيدعم JSONC (comments و trailing commas)
- ممكن تتحكم في الموديلات، الـ permissions، الـ hooks، والـ categories

### الاشتراكات الموصى بيها (لتشغيل أرخص):
- ChatGPT Subscription ($20)
- Kimi Code Subscription ($0.99)
- GLM Coding Plan ($10)

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ بتشتغل على مشاريع كبيرة محتاجة multiple agents بيشتغلوا متوازي
- ✅ بتعمل refactoring كبير في codebase موجود (زي base-layer بتاع شغلك)
- ✅ محتاج تجربة كاملة شبه Cursor/Claude Code بس مفتوحة المصدر
- ✅ عايز توفر في الـ tokens عن طريق توزيع المهام على موديلات أرخص
- ✅ بتحب الـ agentic workflow و الـ orchestration التلقائي

### متستخدمهاش لو:
- ❌ بتعمل tasks بسيطة وسريعة (هتبقى over-engineering)
- ❌ مش عايز تتعامل مع تعدد الـ models والـ agents
- ❌ شغلك بسيط ومحتاج plugin خفيف بس
- ❌ بتشتغل على project صغير ومفيش حاجة معقدة

---

## ⚠️ ملاحظات مهمة

1. **التداخل مع plugins تانية**: لو هتستخدمها مع `opencode-supermemory`، لازم تعطل الـ auto-compact hook بتاعها.
2. **الـ Conductor synergy**: بتشتغل كويس مع `opencode-conductor` كـ Technical Lead.
3. **الترخيص**: SUL-1.0 (license خاص بيهم).
4. **الإلغاء**: لو حبيت تشيلها، لازم تمسح من الـ config + ملفات الـ config التابعة ليها.

---

## 🔗 روابط مفيدة

- README: https://github.com/code-yeongyu/oh-my-opencode
- Installation Guide: https://github.com/code-yeongyu/oh-my-opencode/blob/dev/docs/guide/installation.md
- Features Documentation: https://github.com/code-yeongyu/oh-my-opencode/blob/dev/docs/reference/features.md
- Configuration: https://github.com/code-yeongyu/oh-my-opencode/blob/dev/docs/reference/configuration.md
