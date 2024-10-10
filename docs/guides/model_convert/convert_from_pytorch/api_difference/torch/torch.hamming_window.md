## [ torch 参数更多 ]torch.hamming_window
### [torch.hamming_window](https://pytorch.org/docs/stable/generated/torch.hamming_window.html)

```python
torch.hamming_window(window_length, periodic=True, alpha=0.54, beta=0.46, *, dtype=None, layout=torch.strided, device=None, requires_grad=False)
```

### [paddle.audio.functional.get_window](https://www.paddlepaddle.org.cn/documentation/docs/zh/2.6/api/paddle/audio/functional/get_window_cn.html#get-window)

```python
paddle.audio.functional.get_window(window, win_length, fftbins=True, dtype='float64')
```

PyTorch 相比 Paddle 支持更多其他参数，具体如下：
### 参数映射

| PyTorch       | PaddlePaddle | 备注                                                   |
| ------------- | ------------ | ------------------------------------------------------ |
| -    | window |  窗函数类型，Pytorch 无此参数，Paddle 需设置为 `hamming`。 |
| window_length  | win_length            | 输入窗口的长度，仅参数名不同。 |
| periodic        | fftbins       | 判断是否返回适用于过滤器设计的对称窗口，功能相反，Pytorch 默认值为 True 时，Paddle 须设置为 False，需要转写。  |
| alpha | -  | 窗函数中非线性部分的衰减速度，Paddle 无此参数，暂无转写方式。  |
| beta | -  | 窗函数中线性部分的衰减速度，Paddle 无此参数，暂无转写方式。  |
| dtype        | dtype | 返回 Tensor 的数据类型。 |
| layout | -   | 表示布局方式， Paddle 无此参数，一般对网络训练结果影响不大，可直接删除。 |
| device | -   | 表示 Tensor 存放设备位置，Paddle 无此参数，需要转写。 |
| requires_grad | - | 表示是否计算梯度， Paddle 无此参数，需要转写。 |

### 转写示例

#### window：窗函数类型
```python
# PyTorch 写法
torch.hamming_window(10, periodic = True)

# Paddle 写法
paddle.audio.functional.get_window('hamming', 10, fftbins = False)
```

#### periodic：判断是否返回适用于过滤器设计的对称窗口
```python
# PyTorch 写法
torch.hamming_window(10, periodic = False)

# Paddle 写法
paddle.audio.functional.get_window('hamming', 10, fftbins = True)
```

#### requires_grad：是否需要求反向梯度，需要修改该 Tensor 的 stop_gradient 属性
```python
# PyTorch 写法
torch.hamming_window(10, requires_grad=True)

# Paddle 写法
x = paddle.audio.functional.get_window('hamming', 10, fftbins = False)
x.stop_gradient = False
```

#### device: Tensor 的设备
```python
# PyTorch 写法
torch.hamming_window(10, device=torch.device('cpu'))

# Paddle 写法
y = paddle.audio.functional.get_window('hamming', 10, fftbins = False)
y.cpu()
```