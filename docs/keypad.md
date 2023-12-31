# keypad

操作键盘按键

## 接口目录

- [GetKeyState](#getkeystate): 获取指定的按键状态
- [KeyDown](#keydown): 按住指定的虚拟键码
- [KeyDownChar](#keydownchar): 按住指定的键码名称
- [KeyUp](#keyup): 弹起来虚拟键
- [KeyUpChar](#keyupchar): 弹起来按键名称
- [WaitKey](#waitkey): 等待指定的按键按下
- [KeyPress](#keypress): 按住指定的虚拟键码
- [KeyPressChar](#keypresschar): 按住指定的按键名称

## 接口方法

### GetKeyState

获取指定的按键状态.(前台信息,不是后台)

```c
long GetKeyState(vk_code)
```

| 参数    | 类型 | 描述       |
| ------- | ---- | ---------- |
| vk_code | int  | 虚拟按键码 |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

```c
op.GetKeyState(13)
```

### KeyDown

按住指定的虚拟键码

```c
long KeyDown(vk_code)
```

| 参数    | 类型 | 描述       |
| ------- | ---- | ---------- |
| vk_code | int  | 虚拟按键码 |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

```c
op.KeyDown(13)
```

### KeyDownChar

按住指定的虚拟键码,字符串形式

```c
long KeyDownChar(key_str)
```

| 参数    | 类型   | 描述                                                             |
| ------- | ------ | ---------------------------------------------------------------- |
| key_str | string | 字符串描述的键码,大小写无所谓，按键具体对应关系[按键码](keycode) |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

```c
op.KeyDownChar("enter")
op.KeyDownChar("1")
op.KeyDownChar("F1")
op.KeyDownChar("a")
op.KeyDownChar("B")
```

### KeyUp

弹起来虚拟键 vk_code

```c
long KeyUp(vk_code)
```

| 参数    | 类型 | 描述       |
| ------- | ---- | ---------- |
| vk_code | int  | 虚拟按键码 |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

```c
op.KeyUp(13)
```

### KeyUpChar

弹起来虚拟键,字符串形式

```c
long KeyUpChar(key_str)
```

| 参数    | 类型   | 描述                                                                 |
| ------- | ------ | -------------------------------------------------------------------- |
| key_str | string | 字符串描述的键码,大小写无所谓，按键具体对应关系查看[按键码](keycode) |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

```c
op.KeyUpChar("enter")
op.KeyUpChar("1")
op.KeyUpChar("F1")
op.KeyUpChar("a")
op.KeyUpChar("B")
```

### WaitKey

等待指定的按键按下 (前台,不是后台)

```c
long WaitKey(vk_code,time_out)
```

| 参数     | 类型   | 描述                                                                                 |
| -------- | ------ | ------------------------------------------------------------------------------------ |
| vk_code  | int    | 虚拟按键码,当此值为：0，表示等待任意按键。 鼠标左键是：1,鼠标右键时：2,鼠标中键是：4 |
| time_out | string | 等待多久,单位毫秒. 如果是 0，表示一直等待                                            |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

```c
op.WaitKey(66,0)
```

### KeyPress

按住指定的虚拟键码

```c
long KeyPress(vk_code)
```

| 参数    | 类型 | 描述       |
| ------- | ---- | ---------- |
| vk_code | int  | 虚拟按键码 |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

```c
op.KeyPress(13)
```

### KeyPressChar

按住指定的虚拟键码,字符串形式

```c
long KeyPressChar(key_str)
```

| 参数    | 类型   | 描述                                                                 |
| ------- | ------ | -------------------------------------------------------------------- |
| key_str | string | 字符串描述的键码,大小写无所谓，按键具体对应关系查看[按键码](keycode) |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

```c
op.KeyPressChar("enter")
op.KeyPressChar("1")
op.KeyPressChar("F1")
op.KeyPressChar("a")
op.KeyPressChar("B")
```

## KeyCode

在这里可以找对对应的虚拟按键码和 key_str 参数值

| 键盘按键 | 虚拟键码 |
| -------- | -------- |
| 1        | 49       |
| 2        | 50       |
| 3        | 51       |
| 4        | 52       |
| 5        | 53       |
| 6        | 54       |
| 7        | 55       |
| 8        | 56       |
| 9        | 57       |
| 0        | 48       |
| -        | 189      |
| =        | 187      |
| back     | 8        |
| a        | 65       |
| b        | 66       |
| c        | 67       |
| d        | 68       |
| e        | 69       |
| f        | 70       |
| g        | 71       |
| h        | 72       |
| i        | 73       |
| j        | 74       |
| k        | 75       |
| l        | 76       |
| m        | 77       |
| n        | 78       |
| o        | 79       |
| p        | 80       |
| q        | 81       |
| r        | 82       |
| s        | 83       |
| t        | 84       |
| u        | 85       |
| v        | 86       |
| w        | 87       |
| x        | 88       |
| y        | 89       |
| z        | 90       |
| ctrl     | 17       |
| alt      | 18       |
| shift    | 16       |
| win      | 91       |
| space    | 32       |
| cap      | 20       |
| tab      | 9        |
| ~        | 192      |
| esc      | 27       |
| enter    | 13       |
| up       | 38       |
| down     | 40       |
| left     | 37       |
| right    | 39       |
| option   | 93       |
| print    | 44       |
| delete   | 46       |
| home     | 36       |
| end      | 35       |
| pgup     | 33       |
| pgdn     | 34       |
| f1       | 112      |
| f2       | 113      |
| f3       | 114      |
| f4       | 115      |
| f5       | 116      |
| f6       | 117      |
| f7       | 118      |
| f8       | 119      |
| f9       | 120      |
| f10      | 121      |
| f11      | 122      |
| f12      | 123      |
| [        | 219      |
| ]        | 221      |
| \|\      | 220      |
| ;        | 186      |
| '        | 222      |
| ,        | 188      |
| .        | 190      |
| /        | 191      |
