# Parasail AI Provider Design

## Overview

Add Parasail AI as a new provider with 4 models: MiniMax-M2.5, GLM-4.7-FP8, GLM-5-FP8, and Kimi-K2.5.

## Provider Configuration

**File**: `providers/parasail/provider.toml`

```toml
name = "Parasail AI"
env = ["PARASAIL_API_KEY"]
npm = "@ai-sdk/openai-compatible"
doc = "https://docs.parasail.io"
api = "https://api.saas.parasail.io/v1"
```

## Model Configurations

### 1. MiniMaxAI/MiniMax-M2.5
**File**: `providers/parasail/models/minimaxai-minimax-m2.5.toml`

Based on `providers/minimax/models/MiniMax-M2.5.toml`:
- Context: 204,800 | Output: 131,072
- Capabilities: reasoning, temperature, tool_call
- Pricing: Unknown (TBD)

### 2. zai-org/GLM-4.7-FP8
**File**: `providers/parasail/models/zai-org-glm-4.7-fp8.toml`

Based on `providers/zai/models/glm-4.7.toml`:
- Context: 204,800 | Output: 131,072
- Pricing: $0.45 input / $2.10 output (per 1M tokens)
- Reasoning field: `reasoning_content`

### 3. zai-org/GLM-5-FP8
**File**: `providers/parasail/models/zai-org-glm-5-fp8.toml`

Based on `providers/zai/models/glm-5.toml`:
- Context: 204,800 | Output: 131,072
- Pricing: $1.00 input / $3.20 output
- Reasoning field: `reasoning_content`

### 4. moonshotai/Kimi-K2.5
**File**: `providers/parasail/models/moonshotai-kimi-k2.5.toml`

Based on existing Kimi-K2.5 entries:
- Context: 200,000+ (use 200K default)
- Pricing: $0.60 input / $2.80 output

## Logo

Create `providers/parasail/logo.svg`. Use Parasail brand colors (purple/blue gradient).

## Implementation Steps

1. Create provider directory: `providers/parasail/`
2. Add `provider.toml`
3. Add `logo.svg`
4. Add 4 model TOML files
5. Run `bun validate` to verify
6. Build web: `cd packages/web && bun run build`