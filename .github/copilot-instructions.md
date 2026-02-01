# Repository instructions for GitHub Copilot

This repository defines the **browser-onnx** skill: high-performance local ML inference in the browser using ONNX Runtime Web.

When the user is implementing or debugging browser-based ONNX inference, image classification, object detection, or client-side NLP without a server:

- Use **onnxruntime-web**: `npm install onnxruntime-web`. Configure `ort.env` (e.g. `wasm.numThreads`, `wasm.proxy`, `wasm.wasmPaths`, `webgpu.profiling`).
- Create sessions with `executionProviders: ['webgpu', 'wasm']` and `graphOptimizationLevel: 'all'`.
- Preprocess inputs to match the model (e.g. NCHW); use JIMP or OpenCV.js for images (resize, normalize, RGBA→RGB); build feeds with `new ort.Tensor('float32', data)`.
- Prefer graph capture on WebGPU for static shapes; use IO binding for transformers; use uint8 quantized models on CPU.
- For models >2GB, use external data and `externalData` in session options.
- Call `tensor.dispose()` for GPU tensors; account for mobile thermal throttling with smaller models.

For full steps and examples, see `.cursor/skills/SKILL.md` in this repo.
