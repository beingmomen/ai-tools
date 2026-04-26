# @mohak34/opencode-notifier

> النوع: Notifications Plugin  
> الـ Repo: https://github.com/mohak34/opencode-notifier  
> الـ NPM: `@mohak34/opencode-notifier`  
> الـ Stars: 239+ ⭐

---

## 1. إيه هي الإضافة دي؟

**opencode-notifier** هي plugin بيعمل **desktop notifications + sounds** لما يحصل أي حدث مهم في الـ OpenCode session بتاعتك. بتشتغل على macOS، Linux، و Windows.

الفكرة بسيطة: لما الـ AI agent يشتغل على مهمة طويلة، إنت ممكن تروح تعمل حاجة تانية وترجع لما الشغل يخلص أو يحتاج إذن منك.

### الأحداث اللي بتنبهك عليها:

- 🔔 **Permission** — لما الـ agent محتاج إذنك يعمل حاجة
- ✅ **Complete** — لما الـ session تخلص
- ❌ **Error** — لما يحصل error
- ❓ **Question** — لما الـ agent يسأل سؤال
- 🤖 **Subagent Complete** (silent بشكل افتراضي) — لما subagent يخلص

---

## 2. في ماذا تستخدم؟

استخدمها عشان:

- ✅ **متضيعش وقت** بتقعد تبص على الشاشة منتظر الـ agent يخلص
- ✅ **تشتغل على حاجة تانية** بينما الـ AI شغال على مهمة طويلة
- ✅ **تتنبه فوراً** لو الـ agent محتاج إذن (عشان متعطلش الـ workflow)
- ✅ **تخصص الأصوات** لكل نوع حدث (مثلاً صوت مزعج للـ errors، صوت هادي للـ completion)
- ✅ **تشغل scripts custom** لما يحصل حدث (مثلاً تسجيل في log، تبعت Slack message، إلخ)
- ✅ **تخصص حجم الصوت** لكل event على حدا
- ✅ **dynamic placeholders** زي `{sessionTitle}`, `{projectName}`

---

## 3. كيف تستخدم؟

### التثبيت

في `opencode.json`:

```json
{
  "plugin": ["@mohak34/opencode-notifier@latest"]
}
```

ثم restart الـ OpenCode. خلاص.

### إعدادات Platform-specific

#### macOS:
بيشتغل out-of-the-box. الأيقونة هتبقى Script Editor.

#### Linux:
لازم تثبت `libnotify`:

```bash
# Ubuntu/Debian
sudo apt install libnotify-bin

# Fedora
sudo dnf install libnotify

# Arch
sudo pacman -S libnotify
```

وللأصوات، محتاج واحد من: `paplay`, `aplay`, `mpv`, أو `ffplay`.

#### Windows:
بيشتغل out-of-the-box، بس:
- بس `.wav` بيشتغل (مش mp3)
- استخدم paths كاملة زي `C:/Users/You/sounds/alert.wav`

### الإعدادات المتقدمة

اعمل ملف `~/.config/opencode/opencode-notifier.json`:

```json
{
  "sound": true,
  "notification": true,
  "timeout": 5,
  "showProjectName": true,
  "showSessionTitle": false,
  "showIcon": true,
  
  "events": {
    "permission": { "sound": true, "notification": true },
    "complete": { "sound": true, "notification": true },
    "subagent_complete": { "sound": false, "notification": false },
    "error": { "sound": true, "notification": true },
    "question": { "sound": true, "notification": true }
  },
  
  "messages": {
    "permission": "Session needs permission: {sessionTitle}",
    "complete": "Session has finished: {sessionTitle}",
    "error": "Session encountered an error: {sessionTitle}",
    "question": "Session has a question: {sessionTitle}"
  },
  
  "sounds": {
    "permission": "/path/to/alert.wav",
    "complete": "/path/to/done.wav",
    "error": "/path/to/error.wav",
    "question": "/path/to/question.wav"
  },
  
  "volumes": {
    "permission": 0.6,
    "complete": 0.3,
    "error": 1,
    "question": 0.7
  }
}
```

### Custom Commands

ممكن تشغل script بتاعك لما يحصل حدث:

```json
{
  "command": {
    "enabled": true,
    "path": "/bin/bash",
    "args": [
      "-c",
      "echo '[{event}] {message}' >> /tmp/opencode.log"
    ],
    "minDuration": 10
  }
}
```

`minDuration` بيمنع الـ spam لو الـ response كان سريع.

### Linux Grouping (للحد من الإزعاج):

```json
{
  "linux": {
    "grouping": true
  }
}
```

ده بيخلي الـ notification الجديد يستبدل القديم بدل ما يتراكموا. محتاج `notify-send` 0.8+.

---

## 4. متى تستخدم؟

### استخدمها لما:
- ✅ بتعمل long-running tasks مع AI agent
- ✅ بتشتغل على شاشات متعددة وعايز تتنبه لما يحصل حدث
- ✅ بتروح تعمل حاجة تانية بينما الـ agent شغال
- ✅ شغلك بيحتاج permissions كتيرة وعايز تتنبهلها
- ✅ عايز تبني workflow متكامل مع scripts خارجية (Slack, logging, إلخ)

### متستخدمهاش لو:
- ❌ بتشتغل دايماً قدام الشاشة
- ❌ بتعمل tasks سريعة (ثانية أو اتنين)
- ❌ بتشتغل في بيئة headless (server بدون GUI)
- ❌ مش بتحب الأصوات أو الـ notifications

---

## ⚠️ ملاحظات مهمة

### Troubleshooting شائع:

**macOS - مش شايف notifications:**  
System Settings > Notifications > Script Editor — تأكد إنه على "Banners" أو "Alerts".

**Linux - مفيش notifications:**
```bash
# جرب الأمر ده يدوياً
notify-send "Test" "Hello"
```

**Windows - الـ OpenCode بيهنج لما تظهر notifications:**  
ده known issue مع Bun على Windows. استخدم PowerShell popups بدلاً منها (موجود مثال في الـ README).

**Windows WSL - مفيش notifications:**  
WSL مفيش فيها notification daemon. استخدم PowerShell command:

```json
{
  "notification": false,
  "sound": true,
  "command": {
    "enabled": true,
    "path": "powershell.exe",
    "args": ["-Command", "$wshell = New-Object -ComObject Wscript.Shell; $wshell.Popup('{message}', 5, 'OpenCode - {event}', 0+64)"]
  }
}
```

### لو الـ Plugin مش بيشتغل بعد update:

```bash
# Linux/macOS
rm -rf ~/.cache/opencode/node_modules/@mohak34/opencode-notifier

# Windows
Remove-Item -Recurse -Force "$env:USERPROFILE\.cache\opencode\node_modules\@mohak34\opencode-notifier"
```

ثم restart الـ OpenCode.

### الترخيص: MIT

---

## 🔗 روابط مفيدة

- README: https://github.com/mohak34/opencode-notifier
- NPM: https://www.npmjs.com/package/@mohak34/opencode-notifier
- Changelog: https://github.com/mohak34/opencode-notifier/blob/main/CHANGELOG.md
