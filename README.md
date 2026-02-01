> [!CAUTION]
>
> ### ⚠️ Under Development
>
> This project is currently in its early stages. Skills are being improved, feel free to contribute!


# browser-onnx

High-performance local ML inference in the browser using ONNX Runtime Web. Use when you need privacy-first, low-latency, or offline AI (image classification, object detection, NLP) without server-side processing.

## Install

**One command (skills.sh):**
```bash
npx skills add thongnt0208/browser-onnx-skills
```

**By platform:**
- **Cursor** — `.cursor/skills/SKILL.md` (included when you clone or add this repo).
- **Cline** — copy `.clinerules/browser-onnx.md` into your project’s `.clinerules/` folder.
- **Windsurf** — copy `.windsurf/rules/browser-onnx.md` into your project’s `.windsurf/rules/` folder.
- **Antigravity** — `.agent/skills/browser-onnx/SKILL.md` (workspace); or copy to `~/.gemini/antigravity/skills/browser-onnx/` for global.
- **Claude Code** — `.claude/skills/browser-onnx/SKILL.md` (project); or copy to `~/.claude/skills/browser-onnx/` for personal.
- **Gemini CLI** — `.gemini/skills/browser-onnx/SKILL.md` (workspace); or copy to `~/.gemini/skills/browser-onnx/` for user-wide. Enable in `~/.gemini/settings.json`: `"experimental": { "skills": true }`.
- **GitHub Copilot / universal** — `AGENTS.md` and `.github/copilot-instructions.md` apply when this repo is your workspace or you copy them into your repo.

## What it covers

- **Setup** — ORT-Web install, `ort.env` config (WASM threads, proxy worker, WebGPU profiling)
- **Sessions** — Creating sessions with execution providers (`webgpu`, `wasm`), graph optimization
- **Preprocessing** — Image-to-tensor (resize, normalize), building feeds for NCHW-style inputs
- **Optimization** — Graph capture, IO binding for transformers, quantization (uint8 on CPU)
- **Large models** — External data for models >2GB, handling browser ArrayBuffer limits
- **Edge cases** — Memory disposal, zero-sized tensors, thermal throttling on mobile

Requires a browser with WebAssembly (WASM) support; WebGPU optional for GPU acceleration.
