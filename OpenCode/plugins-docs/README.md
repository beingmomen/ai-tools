# OpenCode Plugins - الإضافات المختارة

> توثيق شامل لـ 9 plugins مختارة لـ OpenCode  
> آخر تحديث: 25 أبريل 2026

---

## 📚 الفهرس

| # | الـ Plugin | النوع | الأولوية |
|---|-----------|-------|----------|
| 1 | [oh-my-opencode](./oh-my-opencode.md) | Agent Harness شامل | 🔴 عالية |
| 2 | [opencode-google-antigravity-auth](./opencode-google-antigravity-auth.md) | Free Auth (Gemini/Claude) | 🔴 عالية |
| 3 | [@tarquinen/opencode-dcp](./opencode-dynamic-context-pruning.md) | Token Optimization | 🔴 عالية |
| 4 | [@mohak34/opencode-notifier](./opencode-notifier.md) | Notifications | 🟡 متوسطة |
| 5 | [opencode-conductor-plugin](./opencode-conductor.md) | Workflow / Process | 🔴 عالية |
| 6 | [opencode-supermemory](./opencode-supermemory.md) | Persistent Memory | 🟡 متوسطة |
| 7 | [opencode-workspace](./opencode-workspace.md) | Bundled Harness | 🟢 اختياري |
| 8 | [opencode-background-agents](./opencode-background-agents.md) | Async Delegation | 🟢 اختياري |
| 9 | [opencode-morph-fast-apply](./opencode-morph-fast-apply.md) | Code Editing Speed | 🟡 متوسطة |
| 10 | [octto](./octto.md) | Browser UI Brainstorming | 🟢 اختياري |
| 11 | [@plannotator/opencode](./plannotator-opencode.md) | Visual Plan Review | 🟢 اختياري |

---

## ⚠️ تحذيرات مهمة جداً

### 1. تعارضات معروفة:

#### Auth Plugins (لازم تختار واحد بس):
- ❌ `opencode-google-antigravity-auth`
- ❌ `opencode-antigravity-auth`
- ❌ `opencode-gemini-auth`

استخدم واحد منهم فقط.

#### Harness Plugins (تداخل محتمل):
- `oh-my-opencode` و `opencode-workspace` — كلاهما agent harness شامل
- `opencode-background-agents` موجود بالفعل في `opencode-workspace` (bundle)
- `oh-my-opencode` عنده Background Agents بنفسه

#### Planning Plugins (تداخل محتمل):
- `opencode-conductor` 
- `@plannotator/opencode`
- `octto + micode`

اختار اللي يناسبك من الـ planning workflow.

### 2. الـ Repo المؤرشف:

⚠️ **`opencode-google-antigravity-auth`** اتأرشف في فبراير 2026، وفي تقارير عن حظر حسابات Google.

---

## 🎯 توصيات بناءً على شغلك

بناءً على ملفك (Nuxt 4 developer في Nanosoft، تشتغل على base-layer، detail-oriented):

### الـ Setup الأساسي الموصى به:

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "opencode-google-antigravity-auth",      // مجاني للموديلات
    "@tarquinen/opencode-dcp@latest",        // توفير tokens
    "@mohak34/opencode-notifier@latest",     // تنبيهات
    "opencode-conductor-plugin"              // workflow منظم
  ]
}
```

### Setup للمستوى المتقدم:

```jsonc
{
  "plugin": [
    "oh-my-opencode",                        // الـ harness الشامل
    "opencode-google-antigravity-auth",      // مجاني
    "@tarquinen/opencode-dcp@latest",        // توفير
    "@mohak34/opencode-notifier@latest",     // تنبيهات
    "opencode-supermemory",                  // ذاكرة دائمة
    "github:JRedeker/opencode-morph-fast-apply"  // تعديل سريع
  ]
}
```

> ⚠️ ملحوظة: لو شغلت `oh-my-opencode` + `opencode-supermemory`، عطل الـ auto-compact hook بتاع OmO:  
> ```json
> // في ~/.config/opencode/oh-my-opencode.json
> { "disabled_hooks": ["anthropic-context-window-limit-recovery"] }
> ```

---

## 📖 طريقة استخدام الملفات

كل ملف بيحتوي على:

1. **شرح الإضافة** — إيه هي وفلسفتها
2. **في ماذا تستخدم** — المميزات والاستخدامات
3. **كيف تستخدم** — التثبيت والإعدادات
4. **متى تستخدم** — السيناريوهات المناسبة وغير المناسبة
5. **ملاحظات مهمة** — تنبيهات وتعارضات
6. **روابط مفيدة** — للمزيد من التفاصيل

---

## 🔗 روابط عامة

- OpenCode Docs: https://opencode.ai/docs/
- Plugins Documentation: https://opencode.ai/docs/plugins/
- Ecosystem: https://opencode.ai/docs/ecosystem
- Discord: https://opencode.ai/discord
