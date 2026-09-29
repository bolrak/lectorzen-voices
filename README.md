# LectorZen voices

Model files downloaded on demand by the LectorZen Android app for its offline neural
text-to-speech voices.

## flow_lm_main_pc.onnx (Spanish)

Per-channel INT8 dynamic quantization (MatMul weights only) of `onnx/spanish/flow_lm_main.onnx`
from [KevinAHM/pocket-tts-onnx](https://huggingface.co/KevinAHM/pocket-tts-onnx), which is an ONNX
export of [Pocket TTS](https://huggingface.co/kyutai/pocket-tts) by [Kyutai](https://kyutai.org/).

The published per-tensor INT8 Spanish model loses a lot of intelligibility (≈76% word accuracy
measured with Whisper vs ≈95% for FP32); this per-channel version keeps ≈93% at the same size.

Produced with:

```python
from onnxruntime.quantization import quantize_dynamic, QuantType
quantize_dynamic("flow_lm_main.onnx", "flow_lm_main_pc.onnx", weight_type=QuantType.QInt8,
                 per_channel=True, op_types_to_quantize=["MatMul"])
```

## License

Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/), like the original work.
Attribution: Pocket TTS © Kyutai; ONNX export by KevinAHM; quantized by LectorZen (modified).
Use must comply with the original model's terms (no voice impersonation, no deceptive use).

## kokoro-v1.0.int8.onnx (Spanish voices Dora & Alex)

INT8 ONNX export of [Kokoro-82M](https://huggingface.co/hexgrad/Kokoro-82M) by hexgrad, as published by
[thewh1teagle/kokoro-onnx](https://github.com/thewh1teagle/kokoro-onnx) (release `model-files-v1.0`), unmodified.
Licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).
LectorZen feeds it with its own Spanish grapheme-to-phoneme rules (no espeak-ng is bundled).
