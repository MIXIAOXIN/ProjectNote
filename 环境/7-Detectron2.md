# 1.配置环境

时间：2021年5月

1 创建/进入 anaconda 环境

```
conda activate fb_detectron2  #激活环境

#或者创建环境
#conda create -n env_name      #创建环境
```

2 检查python环境

```
which python
# 确保显示的python的版本位于 /anadonda/bin 下的python
# 我的此时的返回是：
# /home/mxx/anaconda3/envs/fb_detectron2/bin/python
```

3 安装pytorch

```
#查找相关的教程在该虚拟环境中安装pytorch的方法
# 根据自己的硬件情况，到pytorch官网上，下载安装对应版本的pytorch
# 官网： https://pytorch.org/


# 测试pytorch是否安装成功
python
import torch
print(torch.cuda.is_available)
# 若返回 True，则表示pytorch安装成功
```

4 安装CUDA和CUDNN

```
# 安装CUDA

# 查看CUDA是否安装成功
nvdia-smi
nvcc -V

# 安装CUDNN

# 查看CUDNN是否安装成功
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2

```

5 安装cocoapi

```
pip install cython; pip install 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
```

​		可能会遇到错误：

​		pycocotools/_mask.c:547:21: fatal error: maskApi.h: No such file or directory 

​		我的解决方案：

```
conda install Cython
cd cocoapi/PythonAPI
make
sudo python setup.py install
```

​	6 编译detectron

```
cd detectroon2
python setup.py build develop
```

​			此时运行的老版本的detectron2，会遇到一个“AT_CHECK”不兼容的bug，此时 ；解决方案：在出现这个bug的文件头部添加用户宏：

```
#define AT_CHECK TORCH_CHECK
```

​			再次编译，即可通过编译；

# 2 运行标准测试用例

参考相关资料，写instance segmentation的测试用例

测试文件，见：mxx_test.py中

```
# coding=utf-8
# 加载一些基础包以及设置logger
import detectron2
from detectron2.utils.logger import setup_logger
setup_logger()

# 加载其它一些库
import numpy as np
import cv2

# 加载相关工具
from detectron2.engine import DefaultPredictor
from detectron2.config import get_cfg
from detectron2.utils.visualizer import Visualizer
from detectron2.data import MetadataCatalog

if __name__ == '__main__':
    input_path = "input1.jpg"
    output_path = "result_instance_segmentation.jpg"

    # 指定模型的配置配置文件路径及网络参数文件的路径
    # 对于像下面这样写法的网络参数文件路径，程序在运行的时候就自动寻找，如果没有则下载。
    # Instance segmentation model
    model_file_path = "configs/COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_3x.yaml"
    # 此模型从detectron2仓库中下载得到：
    model_weights = "detectron2/model_zoo/COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_3x/model_final_f10217.pkl"

    # 加载图片
    img = cv2.imread(input_path)

    # 创建一个detectron2配置
    cfg = get_cfg()
    # 要创建的模型的名称
    cfg.merge_from_file(model_file_path)
    # 为模型设置阈值
    cfg.MODEL.ROI_HEADS.SCORE_THRESH_TEST = 0.5
    # 加载模型需要的数据
    cfg.MODEL.WEIGHTS = model_weights
    # 基于配置创建一个默认推断
    predictor = DefaultPredictor(cfg)
    # 利用这个推断对加载的影像进行分析并得到结果
    # 对于输出结果格式可以参考这里https://detectron2.readthedocs.io/tutorials/models.html#model-output-format
    outputs = predictor(img)

    # 控制台中输出一些结果
    print(outputs["instances"].pred_classes)
    print(outputs["instances"].pred_boxes)

    # 得到结果后可以使用Visualizer对结果可视化
    # img[:, :, ::-1]表示将BGR波段顺序变成RGB
    # scale表示输出影像的缩放尺度，太小了会导致看不清
    v = Visualizer(img[:, :, ::-1], MetadataCatalog.get(cfg.DATASETS.TRAIN[0]), scale=1.2)
    v = v.draw_instance_predictions(outputs["instances"].to("cpu"))
    # 获得绘制的影像
    result = v.get_image()[:, :, ::-1]
    # 将影像保存到文件
    cv2.imwrite(output_path, result)
```

