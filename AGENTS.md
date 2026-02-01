# AGENTS.md

Guidance for AI coding agents (Claude Code, Cursor, Copilot, Cline, Windsurf, etc.) when working on **browser-based ONNX inference** or when the user asks for privacy-first, low-latency, or offline ML in the browser.

## When to use this skill

- Implementing local ML inference in the browser (image classification, object detection, NLP).
- User needs offline AI, data privacy, or no server-side processing.
- Working with ONNX Runtime Web, WASM, or WebGPU for inference.

## Core guidance

- **Setup:** `npm install onnxruntime-web`. Use `ort.env` for WASM threads, proxy worker, and WASM paths.
- **Sessions:** Create with `executionProviders: ['webgpu', 'wasm']`, `graphOptimizationLevel: 'all'`.
- **Preprocessing:** Match model format (e.g. NCHW); use JIMP/OpenCV.js for images; normalize and build tensors with `ort.Tensor`.
- **Optimization:** Graph capture on WebGPU for static shapes; IO binding for transformers; prefer uint8 on CPU.
- **Large models (>2GB):** Use external data; link via `externalData` in session options.
- **Edge cases:** Dispose GPU tensors; be aware of zero-sized tensors and mobile thermal throttling.

Full procedural details are in `.cursor/skills/SKILL.md`, `.clinerules/browser-onnx.md`, or `.windsurf/rules/browser-onnx.md` depending on your agent.
