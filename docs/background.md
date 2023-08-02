# background

后台

## 接口目录

- [BindWindow](#bindwindow): 绑定窗口
- [UnBindWindow](#unbindwindow): 解除绑定窗口

## 接口方法

### BindWindow

绑定指定的窗口,并指定这个窗口的屏幕颜色获取方式,鼠标仿真模式,键盘仿真模式,以及模式设定.

```c
long BindWindow(hwnd,display,mouse,keypad,mode)
```

| 参数    | 类型   | 描述                      |
| ------- | ------ | ------------------------- |
| hwnd    | int    | 指定的窗口句柄            |
| display | string | 屏幕显示模式,取值定义如下 |
| mouse   | string | 鼠标仿真模式,取值定义如下 |
| keypad  | string | 键盘仿真模式,取值定义如下 |
| mode    | int    | 模式,取值 0、1            |

**display**

| 值         | 描述                                                     |
| ---------- | -------------------------------------------------------- |
| normal     | 正常模式,平常我们用的前台截屏模式                        |
| gdi        | gdi 模式,用于窗口采用 GDI 方式刷新时,此模式占用 CPU 较大 |
| gdi2       | gdi2 模式,此模式兼容性较强,但是速度比 gdi 模式要慢许多   |
| dx         | dx 模式,等同于 dx.d3d9                                   |
| dx2        | dx2 模式,用于窗口采用 dx 模式刷新                        |
| dx.d3d9    | d3d9 模式,使用 d3d9 渲染                                 |
| dx.d3d10   | d3d10 模式,使用 d3d10 渲染                               |
| dx.d3d11   | d3d11 模式,使用 d3d11 渲染                               |
| opengl     | opengl 模式，使用 opengl 渲染的窗口                      |
| opengl.std | 测试中                                                   |
| opengl.nox | opengl 模式，针对最新夜神模拟器的渲染方式，测试中...     |
| opengl.es  | 测试中...                                                |
| opengl.fi  | 测试中...                                                |

**mouse**

| 值      | 描述                                   |
| ------- | -------------------------------------- |
| normal  | 正常模式,平常我们用的前台鼠标模式      |
| windows | Windows 模式,采取模拟 windows 消息方式 |
| dx      | dx 模式                                |

**keypad**

| 值      | 描述                                   |
| ------- | -------------------------------------- |
| normal  | 正常模式,平常我们用的前台键盘模式      |
| windows | Windows 模式,采取模拟 windows 消息方式 |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
// display: 前台 鼠标:前台键盘:前台 模式0
op_ret = op.BindWindow(hwnd,"normal","normal","normal",0)

// display: gdi 鼠标:前台 键盘:前台 模式1
op_ret = op.BindWindow(hwnd,"gdi","normal","normal",1)
```

### UnBindWindow

解除绑定窗口,并释放系统资源

```c
long UnBindWindow()
```

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op_ret = op.UnBindWindow()
```
