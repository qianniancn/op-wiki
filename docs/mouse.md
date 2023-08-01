# mouse

操作鼠标

## 接口目录

- [GetCursorPos](#getcursorpos): 获取鼠标位置
- [MoveR](#mover): 鼠标移动
- [MoveTo](#moveto): 鼠标移动到指定坐标
- [MoveToEx](#movetoex): 鼠标移动到指定随机坐标
- [LeftClick](#leftclick): 按下鼠标左键
- [LeftDoubleClick](#leftdoubleclick): 双击鼠标左键
- [LeftDown](#leftdown): 按住鼠标左键
- [LeftUp](#leftup): 弹起鼠标左键
- [MiddleClick](#middleclick): 按下鼠标中键
- [MiddleDown](#middledown): 按住鼠标中键
- [MiddleUp](#middleup): 弹起鼠标中键
- [RightClick](#rightclick): 按下鼠标右键
- [RightDown](#rightdown): 按住鼠标右键
- [RightUp](#rightup): 弹起鼠标右键
- [WheelDown](#wheeldown): 滚轮向下滚
- [WheelUp](#wheelup): 滚轮向上滚

## 接口方法

### GetCursorPos

获取鼠标位置

```c
long GetCursorPos(x,y)
```

| 参数 | 类型  | 描述                  |
| ---- | ----- | --------------------- |
| x    | int\* | 变参指针: 返回 X 坐标 |
| y    | int\* | 变参指针: 返回 Y 坐标 |

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
var x, y int
op.GetCursorPos(&x,&y)
printf("x:%d,y:%d",x,y)
```

### MoveR

获取鼠标位置

```c
long MoveR(rx,ry)
```

| 参数 | 类型 | 描述                |
| ---- | ---- | ------------------- |
| rx   | int  | 相对于上次的 X 偏移 |
| ry   | int  | 相对于上次的 Y 偏移 |

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.MoveR(rx,ry)
```

### MoveTo

把鼠标移动到目的点(x,y)

```c
long MoveTo(x,y)
```

| 参数 | 类型 | 描述   |
| ---- | ---- | ------ |
| x    | int  | X 坐标 |
| y    | int  | Y 坐标 |

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.MoveTo(x,y)
```

### MoveToEx

把鼠标移动到目的范围内的任意一点

```c
string MoveToEx(x,y,w,h)
```

| 参数 | 类型 | 描述              |
| ---- | ---- | ----------------- |
| x    | int  | X 坐标            |
| y    | int  | Y 坐标            |
| w    | int  | 宽度(从 x 计算起) |
| h    | int  | 高度(从 y 计算起) |

**返回值**

类型：`string`

返回要移动到的目标点. 格式为 x,y. 比如 MoveToEx 100,100,10,10,返回值可能是 101,102

**示例**

```c
// 移动鼠标到(100,100)到(110,110)这个矩形范围内的任意一点.
op.MoveToEx(100,100,10,10)
```

注: 此函数的意思是移动鼠标到指定的范围(x,y,x+w,y+h)内的任意随机一点

### LeftClick

按下鼠标左键

```c
long LeftClick()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.LeftClick()
```

### LeftDoubleClick

双击鼠标左键

```c
long LeftDoubleClick()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.LeftDoubleClick()
```

### LeftDown

按住鼠标左键

```c
long LeftDown()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.LeftDown()
```

### LeftUp

弹起鼠标左键

```c
long LeftUp()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.LeftUp()
```

### MiddleClick

按下鼠标中键

```c
long MiddleClick()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.MiddleClick()
```

### MiddleDown

按住鼠标中键

```c
long MiddleDown()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.MiddleDown()
```

### MiddleUp

弹起鼠标中键

```c
long MiddleUp()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.MiddleUp()
```

### RightClick

按下鼠标右键

```c
long RightClick()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.RightClick()
```

### RightDown

按住鼠标右键

```c
long RightDown()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.RightDown()
```

### RightUp

弹起鼠标右键

```c
long RightUp()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.RightUp()
```

### WheelDown

滚轮向下滚

```c
long WheelDown()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.WheelDown()
```

### WheelUp

滚轮向下滚

```c
long WheelUp()
```

**返回值**

类型：`int`

- 0：成功
- 1：失败

**示例**

```c
op.WheelUp()
```
