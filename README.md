# Neural-Network-and-Deep-Learning-Project-2

本项目基于 PyTorch 实现，围绕 CIFAR-10 图像分类任务，主要包括两大部分：

1. CIFAR-10 模型建立与训练
2. VGG-A 网络中 Batch Normalization 的研究与可视化

```
项目结构：

codes/
├── cifar10/                            # cifar10数据集
├── myclassifier/                       # Part1 相关代码
│   ├── curve/
│   │   └──*.txt                        # txt文件保存了各个模型训练时的train loss,train acc,val loss,val acc
│   ├── best_models/
│   │   └──*.pth                        # pth文件保存了各个模型权重文件
│   └── *.ipynb                         # 不同损失，激活函数，优化器，模型的训练以及训练曲线，模型可视化
├── VGG_BatchNorm/                      # Part2 相关代码
│   ├── data/                           # 数据集和加载方法
│   ├── grad_path/                      # 训练时保存的梯度文件
│   ├── loss_path/                      # batch级别的训练损失
│   ├── models/                         # 包含VGG-A,VGG-A-batchnorm等模型的定义
│   ├── train_acc_path/                 # 训练时保存的训练准确率
│   ├── train_loss_path/                # epoch级别的训练损失
│   ├── utils/                          # 相关工具,如打印模型权重
│   ├── best_models/                    # 模型权重文件
│   └── val_acc_path/                   # 训练时保存的测试准确率
├── Loss_Landscape.ipynb                # loss和grad的曲线展示(有无BN的对比)
├── parameters.ipynb                    # 模型参数量
├── VGG_Loss_Landscape.ipynb            # VGG-A的训练以及相关曲线
├── VGG_Loss_Landscape.py               # 助教给的模版，没有实际使用，具体见ipynb文件
├── VGG_Loss_Landscape_Batchnorm.ipynb  # VGG-A-BN的训练以及相关曲线
└── VGG_Loss_Landscape_dropout.ipynb    # VGG-A-dropout的训练以及相关曲线

其中cifar10/，myclassifier/best_models/，VGG_BatchNorm/grad_path/，VGG_BatchNorm/best_models/文件太大，
你可以在https://drive.google.com/drive/folders/1wT_jLHLG8UaLFbdjlCeQzftIUemgcjV7?dmr=1&ec=wgc-drive-hero-goto找到它们

```

下面的表格是part1的相关结果，其中最优模型是best_model_adamW_bigger ，测试准确率达到了0.9242

| 模型名称                        | Epochs | Batch Size | Optimizer | Weight Decay | 激活函数        | 学习率 (lr) | 最终训练准确率 | 最终验证准确率 | 测试集最佳准确率 |
| --------------------------- | ------ | ---------- | --------- | ------------ | ----------- | -------- | ------- | ------- | -------- |
| best\_model1                | 100    | 128        | adam      | none         | relu        | 0.001    | 0.9945  | 0.9188  | 0.914    |
| best\_model2                | 100    | 128        | adam      | 0.001        | relu        | 0.001    | 0.9116  | 0.8366  | 0.8732   |
| best\_model\_SGD            | 100    | 128        | SGD       | none         | relu        | 0.001    | 0.8834  | 0.8096  | 0.8128   |
| best\_model\_leakyrelu      | 100    | 128        | adam      | none         | leaky\_relu | 0.001    | 0.9919  | 0.9172  | 0.9137   |
| best\_model\_sigmoid        | 100    | 128        | adam      | none         | sigmoid     | 0.001    | 0.9778  | 0.7074  | 0.8365   |
| best\_model\_adamW          | 100    | 128        | adamW     | none         | relu        | 0.001    | 0.9926  | 0.9098  | 0.9161   |
| best\_model\_adamW\_weight1 | 100    | 128        | adamW     | 0.0001       | relu        | 0.001    | 0.9930  | 0.9192  | 0.9163   |
| best\_model\_adamW\_weight2 | 100    | 128        | adamW     | 0.01         | relu        | 0.001    | 0.9922  | 0.9172  | 0.9156   |
| best\_model\_adamW\_bigger  | 100    | 128        | adamW     | 0.0001       | relu        | 0.001    | 0.9958  | 0.9296  | 0.9242   |
| best\_model\_light          | 100    | 128        | adamW     | 0.0001       | relu        | 0.001    | 0.9872  | 0.9028  | 0.9018   |
