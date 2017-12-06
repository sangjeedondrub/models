# env

```bash
conda create -n tensorflow-models anaconda
source activate tensorflow-models
which python
which pip

# install tensorflow 1.4
pip install \
  -i https://pypi.tuna.tsinghua.edu.cn/simple/ \
  https://mirrors.tuna.tsinghua.edu.cn/tensorflow/linux/cpu/tensorflow-1.4.0-cp36-cp36m-linux_x86_64.whl
```

# compile ops

```bash
TF_INC=$(python -c 'import tensorflow as tf; print(tf.sysconfig.get_include())')
TF_LIB=$(python -c 'import tensorflow as tf; print(tf.sysconfig.get_lib())')
g++ -std=c++11 -shared word2vec_ops.cc word2vec_kernels.cc -o word2vec_ops.so -fPIC -I $TF_INC -I $TF_INC/external/nsync/public/ -L$TF_LIB -ltensorflow_framework -O2 -D_GLIBCXX_USE_CXX11_ABI=0
```

" -D_GLIBCXX_USE_CXX11_ABI=0 " works on my system.


# train

```
python word2vec_optimized.py \
  --train_data=text8 \
  --eval_data=questions-words.txt \
  --save_path=train
  ```


g++ -std=c++11 -shared word2vec_ops.cc word2vec_kernels.cc -o word2vec_ops.so -fPIC -I $TF_INC -I $TF_INC/external/nsync/public -L $TF_LIB -O2 -D_GLIBCXX_USE_CXX11_ABI=0

g++ -std=c++11 -shared -o roi_pooling.so roi_pooling_op.cc -D_GLIBCXX_USE_CXX11_ABI=0 \
roi_pooling_op.cu.o -I $TF_INC -L $TF_LIB -ltensorflow_framework -D GOOGLE_CUDA=1 \
-fPIC $CXXFLAGS -lcudart -L $CUDA_PATH/lib64