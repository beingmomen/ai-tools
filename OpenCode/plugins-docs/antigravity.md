````md
## Option B: Manual Setup

### 1. Add the plugin

Add the plugin to your config file:

`~/.config/opencode/opencode.json`

```json
{
  "plugin": ["opencode-antigravity-auth@latest"]
}
````

> Want bleeding-edge features? Use:
> `opencode-antigravity-auth@beta`

---

### 2. Login with your Google account

```bash
opencode auth login
```

---

### 3. Add models (choose one)

#### Option A (recommended — automatic)

Run:

```bash
opencode auth login
```

Then follow:

* Google
* OAuth with Google (Antigravity)
* Select **"Configure models in opencode.json"**

This will auto-configure all models.

#### Option B (manual)

Copy the full configuration manually into your config file.

---

### 4. Use it

```bash
opencode run "Hello" --model=google/antigravity-claude-opus-4-6-thinking --variant=max
```

```
```
