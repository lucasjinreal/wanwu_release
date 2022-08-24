# Wanwu

Only for host some model weights on github.


## FAQ

Q: What's backend switch difference with ONNXRuntime?

A: We are not using onnxruntime for backend switch, we don't support bare CUDA on GPU, only support TensorRT, since we **only using the fastest way on target platform**. For CPU, we using 


Q: Error: `anaconda3/envs/dl/bin/../lib/libstdc++.so.6: version `GLIBCXX_3.4.29' not found`?

A: this can be got when you using anaconda and a very decent g++ (like Ubuntu 21.10). if `strings  ~/anaconda3/envs/dl/bin/../lib/libstdc++.so.6 | grep GLIBCXX_3.4.29` you will found this returned null. 
You can try: `strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep LIBCXX`, and copy system libstdc++ to conda. After that, problem can be solved.


## Copyright

All rights reserved by Lucas Jin @2022

 
