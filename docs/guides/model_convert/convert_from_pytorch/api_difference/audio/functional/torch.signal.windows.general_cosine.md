## [ torch 参数更多 ]torch.signal.windows.general_cosine
### [torch.signal.windows.general_cosine](https://pytorch.org/docs/stable/generated/torch.signal.windows.general_cosine.html)

```python
torch.signal.windows.general_cosine(M, *, a, sym=True, dtype=None, layout=torch.strided, device=None, requires_grad=False)
```

### [paddle.audio.functional.get_window](https://www.paddlepaddle.org.cn/documentation/docs/zh/2.6/api/paddle/audio/functional/get_window_cn.html#get-window)

```python
paddle.audio.functional.get_window(window, win_length, fftbins=True, dtype='float64')
```

PyTorch 相比 Paddle 支持更多其他参数，具体如下：
### 参数映射

| PyTorch       | PaddlePaddle | 备注                                                   |
| ------------- | ------------ | ------------------------------------------------------ |
| - | window |  窗函数类型，Pytorch 无此参数，Paddle 需设置为 `general_cosine`。 |
| M  | win_length            | 输入窗口的长度，也是采样点数，仅参数名不一致。 |
| a         | -           | 与每个余弦函数相关的系数。Paddle 无此参数，需要转写。|
| sym        | fftbins       | 判断是否返回适用于过滤器设计的对称窗口，功能相反，Pytorch 默认值为 True 时，Paddle 须设置为 False，需要转写。  |
| dtype        | dtype | 返回 Tensor 的数据类型，支持 float32、float64。PyTorch 若参数为空，返回数据类型默认为 `float32`。 Paddle 若参数为空，返回数据类型默认为 `float64` ，需要转写。|
| layout | -   | 表示布局方式， Paddle 无此参数，一般对网络训练结果影响不大，可直接删除。 |
| device | -   | 表示 Tensor 存放设备位置，Paddle 无此参数，需要转写。 |
| requires_grad | - | 表示是否计算梯度， Paddle 无此参数，需要转写。 |

### 转写示例

#### window：窗函数类型
```python
# PyTorch 写法
torch.signal.windows.general_cosine(10, a=[0.46, 0.23, 0.31])

# Paddle 写法
paddle.audio.functional.get_window(('general_cosine', [0.46, 0.23, 0.31]), 10, fftbins = False)
```

#### sym：判断是否返回适用于过滤器设计的对称窗口
```python
# PyTorch 写法
torch.signal.windows.general_cosine(10, a=[0.46, 0.23, 0.31])

# Paddle 写法
paddle.audio.functional.get_window(('general_cosine', [0.46, 0.23, 0.31]), 10, fftbins = False)
```

```python
# PyTorch 写法
torch.signal.windows.general_cosine(10, a=[0.46, 0.23, 0.31], sym=False)

# Paddle 写法
paddle.audio.functional.get_window(('general_cosine', [0.46, 0.23, 0.31]), 10, fftbins = True)
```

#### a：余弦函数相关的系数
```python
# PyTorch 写法
torch.signal.windows.general_cosine(10, a=[0.5, 1 - 0.5])

# Paddle 写法
paddle.audio.functional.get_window(('general_cosine', [0.5, 1 - 0.5]), 10, fftbins = False)
```

#### dtype：返回 Tensor 的数据类型
```python
# PyTorch 写法
torch.signal.windows.general_cosine(10, a=[0.46, 0.23, 0.31])

# Paddle 写法
paddle.audio.functional.get_window(('general_cosine', [0.46, 0.23, 0.31]), 10, dtype='float32', fftbins = False)
```

#### requires_grad：是否需要求反向梯度，需要修改该 Tensor 的 stop_gradient 属性
```python
# PyTorch 写法
torch.signal.windows.general_cosine(10, a=[0.46, 0.23, 0.31], requires_grad=True)

# Paddle 写法
x = paddle.audio.functional.get_window(('general_cosine', [0.46, 0.23, 0.31]), 10, fftbins = False)
x.stop_gradient = False
```

#### device: Tensor 的设备
```python
# PyTorch 写法
torch.signal.windows.general_cosine(10, a=[0.46, 0.23, 0.31], device=torch.device('cpu'))

# Paddle 写法
y = paddle.audio.functional.get_window(('general_cosine', [0.46, 0.23, 0.31]), 10, fftbins = False)
y.cpu()
```
