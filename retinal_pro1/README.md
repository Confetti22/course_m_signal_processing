# 现代信号处理 project1

# task1 model demo:

### model

 u-net with features:64,128,256,512,1024

这个5层的u-net对于当前眼底照片的数据量来说，参数量足够大，应该不存在model bias

探究的点： 使用其他更好的分割模型，并可尝试数据增强

### loss 曲线

loss function: dice loss

### Train loss with validation

![Untitled](%E7%8E%B0%E4%BB%A3%E4%BF%A1%E5%8F%B7%E5%A4%84%E7%90%86%20project1%2051db5d3688a04c438d084819476ea033/Untitled.png)

### train loss  without validation:

![Untitled](%E7%8E%B0%E4%BB%A3%E4%BF%A1%E5%8F%B7%E5%A4%84%E7%90%86%20project1%2051db5d3688a04c438d084819476ea033/Untitled%201.png)

进行了validation后，可以看到模型的loss没有收敛的很好，但是有validation 的model (w_val)在hd95,assd上的表现都远远好于没有validation 的model(wo_val), 对于dice系数，有没有val的效果都差不多。

可以探究的点：使用三种指标的混合loss效果会如何，如何设定这个混合loss函数，或者使用其他更好的loss函数？

### model performance on all five domain （左边：w_val, 右边：wo_val）

---

![Untitled](%E7%8E%B0%E4%BB%A3%E4%BF%A1%E5%8F%B7%E5%A4%84%E7%90%86%20project1%2051db5d3688a04c438d084819476ea033/Untitled%202.png)

![Untitled](%E7%8E%B0%E4%BB%A3%E4%BF%A1%E5%8F%B7%E5%A4%84%E7%90%86%20project1%2051db5d3688a04c438d084819476ea033/Untitled%203.png)

奇怪的点：

在domain1上训练的模型在domain2上表现最好(全部3个指标都更好)，要探究这个问题吗，如何探究？

### 分割效果

以下为部分分割效果

model: domain1_w_val4.pth; prediction on domain1 test:

![Untitled](%E7%8E%B0%E4%BB%A3%E4%BF%A1%E5%8F%B7%E5%A4%84%E7%90%86%20project1%2051db5d3688a04c438d084819476ea033/Untitled%204.png)

![Untitled](%E7%8E%B0%E4%BB%A3%E4%BF%A1%E5%8F%B7%E5%A4%84%E7%90%86%20project1%2051db5d3688a04c438d084819476ea033/Untitled%205.png)

![Untitled](%E7%8E%B0%E4%BB%A3%E4%BF%A1%E5%8F%B7%E5%A4%84%E7%90%86%20project1%2051db5d3688a04c438d084819476ea033/Untitled%206.png)

可探究的点：

可以看到模型没有很好的学到眼底的特征： 亮度低，近似圆形，单一的连通区域，大致位于图像中央

模型只很好的学到了亮度低 这个特征，是否可以根据上述的特征作为先验，限制模型要识别到这些特征？或者如何更好的让模型学到更多重要的特征？
