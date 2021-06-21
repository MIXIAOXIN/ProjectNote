# Point3d 环境搭建

1 创建新的虚拟环境

```
conda create -n point3d python=3.6
conda activate point3d
# cuda 版本为10.1
conda install pytorch torchvision cudatoolkit=10.1 -c pytorch
#这一步好像挺重要：
？无
```

2 测试环境是否可用

```
python
import numpy
import torch
# 可能出现错误：找不到mkl_thread.so之类的错误
# 不清楚错误出现的原因，尝试了
# conda update numpy
# conda update mkl
# 均没有解决问题
# 再次尝试以下命令，查找这些库所在的位置：
sudo find /home. -name mkl_threas.so
# 查找到这个库所在的位置，发现在其他虚拟环境中有这个库文件，不知道为什么这个新建的环境中没有这个库文件??
# 将找到的库文件，拷贝到当前虚拟环境的库目录下
cp /home/mxx/anaconda3/lib/mkl_thread.so /home/mxx/anaconda3/env/point3d/lib/.

# 发现有好几个链接库都找不到，用同样的方法，拷贝到当前目录下。
python
print(torch.__version__）
#  1.7.1
print(torch.cuda.is_available())
# 返回True
```

3 根据Points3d官网介绍安装依赖库

```
pip install torch
#若出现错误：没有pip之类的，根据错误提示，安装pip库
#参考：https://blog.csdn.net/weixin_42069606/article/details/104914037
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py --force-reinstall

#之后便安装torch-points3d
pip install torch-point3d

```

4 测试demo样例

