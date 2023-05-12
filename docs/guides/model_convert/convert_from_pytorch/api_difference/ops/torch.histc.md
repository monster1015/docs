## [ torch 参数更多]torch.histc

### [torch.histc](https://pytorch.org/docs/1.13/generated/torch.histc.html#torch-histc)

```python
torch.histc(input, bins=100, min=0, max=0, *, out=None)
```

### [paddle.histogram](https://www.paddlepaddle.org.cn/documentation/docs/zh/api/paddle/histogram_cn.html#histogram)

```python
paddle.histogram(input, bins=100, min=0, max=0, name=None)
```

其中 PyTorch 相比 Paddle 支持更多其他参数，具体如下：

### 参数映射

| PyTorch | PaddlePaddle | 备注                                                |
| ------- | ------------ | --------------------------------------------------- |
| input   | input        | 表示输入的 Tensor。                                  |
| bins    | bins         | 表示直方图直条的个数。                              |
| min     | min          | 表示范围的下边界。                                  |
| max     | max          | 表示范围的上边界。                                  |
| out     | -            | 表示输出的 Tensor，Paddle 无此参数，需要进行转写。 |

### 转写示例

#### out：指定输出

```python
# Pytorch 写法
torch.histc(x, out=y)

# Paddle 写法
paddle.assign(paddle.histogram(x), y)
```