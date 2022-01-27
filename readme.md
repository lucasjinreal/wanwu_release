# Wanwu

![](https://s4.ax1x.com/2022/01/09/7kCEtJ.png)

> 可能是世界上最简单直接的模型部署工具，请注意，不依赖PyTorch,所有代码都以最快的方式跑在它应在的平台上


Wanwu is from『万物』. We believe everything in this world are animisim, in Chinese, we have an ancient word says: 万物有灵. **Wanwu** is a Deeplearning framework that provides SOTA and comman used AI models out-of-box. 

Wanwu designed with a principle of **fast**, **less dependencies**, **platform fastest**, **cover common use scenarios**, all models can runs at a very fast speed under our optimization. You can use backend on any of these platforms **with the fastest speed on that target platform**:

- GPU: TensorRT or CUDA;
- CPU: onnxruntime or tvm;

Current supported models are:

- [x] YOLOv5-RT support in TensorRT;
- [ ] YOLOX on coco, you can detect human, birds, cars etc;
- [ ] SCRFD for face detection;


## Install

If you want a fast face detection model, now you don't need FaceBoxes or Dlib, using wanwu, you can specific runs on CPU or GPU or enable TensorRT, any platform you want as long as you have according dependencies:

```
pip install wanwu
```


## Results

![YOLOv5](https://s4.ax1x.com/2022/01/09/7k9ao4.png)

![SCRFD](https://s4.ax1x.com/2022/01/10/7ZCI8e.png)

**note: All speed tested above are runing on GTX1070 (included nms), more decent GPUs could be even more faster.**

## Usage

If you want a detector, just:

```python
from wanwu.det import Det
from wanwu.core.infer import Backends

det = Det(type='yolov5', onnx_f=args.model_file, backend=Backends.GPU_TENSORRT, timing=True)

det.infer(image)
# now the result is bboxes, labels, scores
```

Or, if you want a face detector, and you want runs on CPU:

```python
from wanwu.det import Det
from wanwu.core.infer import Backends

det = Det(type='yolov5', onnx_f=args.model_file, backend=Backends.GPU_TENSORRT, timing=True)

det.infer(image)
# now you can have a fastest SSFD face detection model runs on your CPU
# or you can switch to TensorRT if you want fastest speed on GPU
```

## Problems Known

There still some problems in `wanwu` that we occured. 

- FP16 not supported due to EfficientNMS bug in TensorRT;
- CPU detection model might fail if your model converts from mmdetection;


## Projects Demo used Wanwu

to be done


## FAQ

Q: What's backend switch difference with ONNXRuntime?

A: We are not using onnxruntime for backend switch, we don't support bare CUDA on GPU, only support TensorRT, since we **only using the fastest way on target platform**. For CPU, we using 


Q: Error: `anaconda3/envs/dl/bin/../lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found`?

A: this can be got when you using anaconda and a very decent g++ (like Ubuntu 21.10). if `strings  ~/anaconda3/envs/dl/bin/../lib/libstdc++.so.6 | grep GLIBCXX_3.4.29` you will found this returned null. 
You can try: `strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep LIBCXX`, and copy system libstdc++ to conda. After that, problem can be solved.


## Copyright

All rights reserved by Lucas Jin @2022

 