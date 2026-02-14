# Parasail AI Provider Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add Parasail AI as a new provider with 4 models (MiniMax-M2.5, GLM-4.7-FP8, GLM-5-FP8, Kimi-K2.5)

**Architecture:** Create new provider directory with provider.toml, logo.svg, and 4 model TOML files. Use existing model configs as templates.

**Tech Stack:** Bun, TOML, @ai-sdk/openai-compatible

---

### Task 1: Create provider directory and provider.toml

**Files:**
- Create: `providers/parasail/provider.toml`
- Reference: `providers/zai/provider.toml`

**Step 1: Create directory and provider.toml**

```bash
mkdir -p providers/parasail/models
```

```toml
name = "Parasail AI"
env = ["PARASAIL_API_KEY"]
npm = "@ai-sdk/openai-compatible"
doc = "https://docs.parasail.io"
api = "https://api.saas.parasail.io/v1"
```

**Step 2: Commit**

```bash
git add providers/parasail/
git commit -m "feat: add Parasail AI provider config"
```

---

### Task 2: Create logo.svg

**Files:**
- Create: `providers/parasail/logo.svg`
- Reference: `providers/moonshotai/logo.svg` (for SVG format)

**Step 1: Create simple Parasail logo**

Use Parasail brand colors (purple gradient). Example minimal logo:
```svg
<svg width="24" height="24" viewBox="0 0 40 40" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <linearGradient id="grad" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" style="stop-color:#8B5CF6"/>
      <stop offset="100%" style="stop-color:#3B82F6"/>
    </linearGradient>
  </defs>
  <circle cx="20" cy="20" r="18" fill="url(#grad)"/>
  <path d="M12 20 L20 12 L28 20 L20 28 Z" fill="white"/>
</svg>
```

**Step 2: Commit**

```bash
git add providers/parasail/logo.svg
git commit -m "feat: add Parasail AI logo"
```

---

### Task 3: Add MiniMaxAI/MiniMax-M2.5 model

**Files:**
- Create: `providers/parasail/models/minimaxai-minimax-m2.5.toml`
- Reference: `providers/minimax/models/MiniMax-M2.5.toml`

**Step 1: Create model TOML**

```toml
name = "MiniMaxAI/MiniMax-M2.5"
family = "minimax"
release_date = "2026-02-14"
last_updated = "2026-02-14"
attachment = false
reasoning = true
temperature = true
tool_call = true
open_weights = true

[cost]
input = 0
output = 0

[limit]
context = 204_800
output = 131_072

[modalities]
input = ["text"]
output = ["text"]
```

**Step 2: Commit**

```bash
git add providers/parasail/models/minimaxai-minimax-m2.5.toml
git commit -m "feat(parasail): add MiniMax-M2.5 model"
```

---

### Task 4: Add zai-org/GLM-4.7-FP8 model

**Files:**
- Create: `providers/parasail/models/zai-org-glm-4.7-fp8.toml`
- Reference: `providers/zai/models/glm-4.7.toml`

**Step 1: Create model TOML**

```toml
name = "zai-org/GLM-4.7-FP8"
family = "glm"
release_date = "2026-02-14"
last_updated = "2026-02-14"
attachment = false
reasoning = true
temperature = true
tool_call = true
open_weights = false

[interleaved]
field = "reasoning_content"

[cost]
input = 0.45
output = 2.10

[limit]
context = 204_800
output = 131_072

[modalities]
input = ["text"]
output = ["text"]
```

**Step 2: Commit**

```bash
git add providers/parasail/models/zai-org-glm-4.7-fp8.toml
git commit -m "feat(parasail): add GLM-4.7-FP8 model"
```

---

### Task 5: Add zai-org/GLM-5-FP8 model

**Files:**
- Create: `providers/parasail/models/zai-org-glm-5-fp8.toml`
- Reference: `providers/zai/models/glm-5.toml`

**Step 1: Create model TOML**

```toml
name = "zai-org/GLM-5-FP8"
family = "glm"
release_date = "2026-02-14"
last_updated = "2026-02-14"
attachment = false
reasoning = true
temperature = true
tool_call = true
open_weights = false

[interleaved]
field = "reasoning_content"

[cost]
input = 1.00
output = 3.20
cache_read = 0.20
cache_write = 0

[limit]
context = 204_800
output = 131_072

[modalities]
input = ["text"]
output = ["text"]
```

**Step 2: Commit**

```bash
git add providers/parasail/models/zai-org-glm-5-fp8.toml
git commit -m "feat(parasail): add GLM-5-FP8 model"
```

---

### Task 6: Add moonshotai/Kimi-K2.5 model

**Files:**
- Create: `providers/parasail/models/moonshotai-kimi-k2.5.toml`
- Reference: `providers/nebius/models/moonshotai/Kimi-K2.5.toml` (for context limits)

**Step 1: Create model TOML**

```toml
name = "moonshotai/Kimi-K2.5"
family = "moonshot"
release_date = "2026-02-14"
last_updated = "2026-02-14"
attachment = false
reasoning = true
temperature = true
tool_call = true
open_weights = false

[cost]
input = 0.60
output = 2.80

[limit]
context = 200_000
output = 131_072

[modalities]
input = ["text"]
output = ["text"]
```

**Step 2: Commit**

```bash
git add providers/parasail/models/moonshotai-kimi-k2.5.toml
git commit -m "feat(parasail): add Kimi-K2.5 model"
```

---

### Task 7: Validate and build

**Files:**
- Modify: (none)
- Test: Run validation and build

**Step 1: Run validation**

```bash
bun validate
```

Expected: All 4 Parasail models pass validation

**Step 2: Build web**

```bash
cd packages/web && bun run build
```

Expected: Build succeeds

**Step 3: Final commit**

```bash
git add -A && git commit -m "feat: complete Parasail AI provider with 4 models"
```

---

**Plan complete and saved to `docs/plans/2026-02-14-parasail-ai-implementation.md`. Two execution options:**

1. **Subagent-Driven (this session)** - I dispatch fresh subagent per task, review between tasks, fast iteration

2. **Parallel Session (separate)** - Open new session with executing-plans, batch execution with checkpoints

**Which approach?**