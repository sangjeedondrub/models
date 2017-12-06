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

# compile

```bash
```


g++ -std=c++11 -shared $i -o $o  -fPIC -I$TF_INC -I$TF_INC/external/nsync/public -L$TF_LIB -ltensorflow_framework -O2  -D_GLIBCXX_USE_CXX11_ABI=0


# train

```
python word2vec_optimized.py \
  --train_data=text8 \
  --eval_data=questions-words.txt \
  --save_path=train
  ```