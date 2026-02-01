# Browser-Based ONNX Inference

Use when implementing high-performance local ML inference in the browser with ONNX Runtime Web (privacy-first, low-latency, offline AI: image classification, object detection, NLP). Requires browser with WebAssembly (WASM) support; WebGPU optional for GPU acceleration.

## 1. Setup and Installation

```bash
npm install onnxruntime-web
```
For WebGPU/WebNN: `onnxruntime-web@dev`.

## 2. Global Environment Configuration

Set `ort.env` before creating a session:

- **WASM (CPU):** `ort.env.wasm.numThreads`, `ort.env.wasm.proxy = true` for UI responsiveness.
- **WASM Paths:** `ort.env.wasm.wasmPaths` if binaries are not next to the JS bundle.
- **WebGPU:** `ort.env.webgpu.profiling = { mode: 'default' }` for profiling.

## 3. Creating an Inference Session

```javascript
import * as ort from 'onnxruntime-web';

const session = await ort.InferenceSession.create('./model.onnx', {
  executionProviders: ['webgpu', 'wasm'],
  graphOptimizationLevel: 'all'
});
```

## 4. Data Preprocessing

- **Image-to-Tensor:** JIMP or OpenCV.js — resize, normalize (÷255), RGBA→RGB.
- **Tensor:** `new ort.Tensor('float32', float32Data,)` for input feeds (e.g. NCHW for vision).

## 5. Optimized Inference Patterns

- **Graph Capture:** WebGPU + static shapes → `enableGraphCapture: true`.
- **IO Binding:** Transformers → `ort.Tensor.fromGpuBuffer()`, `preferredOutputLocation: 'gpu-buffer'`.
- **Quantization:** Prefer uint8 on CPU (WASM); avoid float16 on CPU.

## 6. Large Model Handling (>2GB)

Browser ArrayBuffer ~2GB limit → export with **external data**:

```javascript
const session = await ort.InferenceSession.create(modelUrl, {
  externalData: [{ path: './model.data', data: dataUrl }]
});
```

## 7. Edge Cases

- Call `tensor.dispose()` for GPU tensors.
- Zero-sized tensors are treated as CPU.
- Mobile: thermal throttling can double latency — use tiny models.

## 8. Examples

- **Translation:** Web Worker + singleton for heavy models (e.g. NLLB-200).
- **YOLO:** Implement or run a separate NMS ONNX model for overlapping boxes.
