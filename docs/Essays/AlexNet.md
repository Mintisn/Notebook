# AlexNet
[NIPS-2012-imagenet-classification-with-deep-convolutional-neural-networks-Paper](https://papers.nips.cc/paper/2012/file/c399862d3b9d6b76c8436e924a68c45b-Paper.pdf)

## Abstract

## the dataset
alexnet没有直接抽取图片的特征,而是在原始图片raw RGB上做的
## the architecture
+ 使用了ReLU层,而不是tanh,加快网络速度
+ 局部响应归一化（LRN），可以增强模型的泛化能力。
+ 重叠最大池化层，可以减少特征图的大小和过拟合的风险。
+ 分组卷积层，可以在两个GPU上并行训练网络，并减少参数数量。
+ 数据增强技术，可以通过随机裁剪、水平翻转和RGB通道变换来扩充训练数据。  

## Discussion
+ 首先是网络深度比较重要,论文中删除中间层都会使得性能下降2%左右(实际上去掉一些层是没有关系的,如果参数调得好 )
+ 文章最后提到video, 目前为止实际上video 方向的发展仍然比较缓慢