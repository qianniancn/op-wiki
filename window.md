# window

windows 窗口相关操作

## 接口方法

### EnumWindow

根据指定条件,枚举系统中符合条件的窗口

```c
string EnumWindow(parent,title,class_name,filter)
```

| 参数       | 类型   | 描述                            |
| ---------- | ------ | ------------------------------- |
| parent     | int    | 父窗口的句柄                    |
| title      | string | 窗口的标题                      |
| class_name | string | 窗口的类名                      |
| filter     | int    | 表示窗口的过滤条件,可以是以下值 |

**filter**

| 值  | 描述                                  |
| --- | ------------------------------------- |
| 1   | 匹配窗口标题，参数 title 有效         |
| 2   | 匹配窗口类名，参数 class_name 有效    |
| 4   | 只匹配指定父窗口的第一层子窗口        |
| 8   | 匹配所有者窗口为 0 的窗口，即顶级窗口 |
| 16  | 匹配可见的窗口                        |
| 32  | 匹配出的窗口按照窗口打开顺序依次排列  |

这些值可以相加,比如 4+8+16 就是类似于任务管理器中的窗口列表

**返回值**

类型：`string`

返回所有匹配到的窗口句柄

**示例**

无

### EnumWindowByProcess

根据指定进程以及其它条件,枚举系统中符合条件的窗口

```c
string EnumWindowByProcess(process_name,title,class_name,filter)
```

| 参数         | 类型   | 描述                            |
| ------------ | ------ | ------------------------------- |
| process_name | string | 进程名称                        |
| title        | string | 窗口的标题                      |
| class_name   | string | 窗口的类名                      |
| filter       | int    | 表示窗口的过滤条件,可以是以下值 |

**filter**

| 值  | 描述                                  |
| --- | ------------------------------------- |
| 1   | 匹配窗口标题，参数 title 有效         |
| 2   | 匹配窗口类名，参数 class_name 有效    |
| 4   | 只匹配指定父窗口的第一层子窗口        |
| 8   | 匹配所有者窗口为 0 的窗口，即顶级窗口 |
| 16  | 匹配可见的窗口                        |
| 32  | 匹配出的窗口按照窗口打开顺序依次排列  |

这些值可以相加,比如 4+8+16 就是类似于任务管理器中的窗口列表

**返回值**

类型：`string`

返回所有匹配到的窗口句柄

**示例**

无

### EnumProcess

根据指定进程名,枚举系统中符合条件的进程 PID

```c
string EnumProcess(name)
```

| 参数 | 类型   | 描述     |
| ---- | ------ | -------- |
| name | string | 进程名称 |

**返回值**

类型：`string`

返回所有匹配的进程 PID,返回格式："10180,15352,15000,17620,19412"

**示例**

```c
ret=op.EnumProcess("qq.exe")

println(ret)
```

### ClientToScreen

把窗口坐标转换为屏幕坐标

```c
long ClientToScreen(hwnd,x,y)
```

| 参数 | 类型  | 描述                      |
| ---- | ----- | ------------------------- |
| hwnd | int   | 指定的窗口句柄            |
| x    | int\* | 变参指针: 接收窗口 X 坐标 |
| y    | int\* | 变参指针: 接收窗口 Y 坐标 |

**返回值**

类型：`int`

- 0：表示操作成功。
- 1：表示操作失败。

**示例**

```go
var x,y int
ret = op.ClientToScreen(hwnd,x,y)
println(x,y)
```

### FindWindow

查找符合类名或者标题名的顶层可见窗口

```c
long FindWindow(class,title)
```

| 参数  | 类型   | 描述                                              |
| ----- | ------ | ------------------------------------------------- |
| class | string | 窗口类名,如果为空,则匹配所有,这里的匹配是模糊匹配 |
| title | string | 窗口标题,如果为空,则匹配所有,这里的匹配是模糊匹配 |

**返回值**

类型：`int`

返回窗口句柄,没找到则返回 0

**示例**

```c
hwnd = op.FindWindow("","记事本")
```

### FindWindowByProcess

根据指定的进程名字，来查找可见窗口

```c
long FindWindowByProcess(process_name,class,title)
```

| 参数         | 类型   | 描述                                                   |
| ------------ | ------ | ------------------------------------------------------ |
| process_name | string | 进程名,比如(notepad.exe),这里是精确匹配,但不区分大小写 |
| class        | string | 窗口类名,如果为空,则匹配所有,这里的匹配是模糊匹配      |
| title        | string | 窗口标题,如果为空,则匹配所有,这里的匹配是模糊匹配      |

**返回值**

类型：`int`

返回窗口句柄,没找到则返回 0

**示例**

```c
hwnd = op.FindWindowByProcess("noteapd.exe","","记事本")
```

### FindWindowByProcessId

根据指定的进程 Id，来查找可见窗口

```c
long FindWindowByProcessId(process_id,class,title)
```

| 参数       | 类型   | 描述                                              |
| ---------- | ------ | ------------------------------------------------- |
| process_id | int    | 进程 id                                           |
| class      | string | 窗口类名,如果为空,则匹配所有,这里的匹配是模糊匹配 |
| title      | string | 窗口标题,如果为空,则匹配所有,这里的匹配是模糊匹配 |

**返回值**

类型：`int`

返回窗口句柄,没找到则返回 0

**示例**

```c
hwnd = op.FindWindowByProcessId(123456,"","记事本")
```

### FindWindowEx

查找符合类名或者标题名的顶层可见窗口,如果指定了 parent,则在 parent 的第一层子窗口中查找

```c
long FindWindowEx(parent,class,title)
```

| 参数   | 类型   | 描述                                              |
| ------ | ------ | ------------------------------------------------- |
| parent | int    | 父窗口句柄，如果为空，则匹配所有顶层窗口          |
| class  | string | 窗口类名,如果为空,则匹配所有,这里的匹配是模糊匹配 |
| title  | string | 窗口标题,如果为空,则匹配所有,这里的匹配是模糊匹配 |

**返回值**

类型：`int`

返回窗口句柄,没找到则返回 0

**示例**

```c
hwnd = op.FindWindowEx(0,"","记事本")
```

### GetClientRect

获取窗口客户区域在屏幕上的位置

```c
long GetClientRect(hwnd,x1,y1,x2,y2)
```

| 参数 | 类型  | 描述                                  |
| ---- | ----- | ------------------------------------- |
| hwnd | int   | 指定的窗口句柄                        |
| x1   | int\* | 变参指针: 返回窗口客户区左上角 X 坐标 |
| y1   | int\* | 变参指针: 返回窗口客户区左上角 Y 坐标 |
| x2   | int\* | 变参指针: 返回窗口客户区右下角 X 坐标 |
| y2   | int\* | 变参指针: 返回窗口客户区右下角 Y 坐标 |

**返回值**

类型：`int`

- 0:成功
- 1:失败

**示例**

```c
ret = op.GetClientRect(hwnd,x1,y1,x2,y2)
```

### GetClientSize

获取窗口客户区域的宽度和高度

```c
long GetClientSize(hwnd,width,width)
```

| 参数   | 类型  | 描述               |
| ------ | ----- | ------------------ |
| parent | int   | 指定的窗口句柄     |
| width  | int\* | 变参指针: 窗口宽度 |
| width  | int\* | 变参指针: 窗口高度 |

**返回值**

类型：`int`

- 0:成功
- 1:失败

**示例**

```c
var w,h int
op.GetClientSize(hwnd,&w,&h)
printf("宽度:%d,高度:%d",w,h)
```

### GetForegroundFocus

获取顶层活动窗口中具有输入焦点的窗口句柄

```c
long GetForegroundFocus()
```

**返回值**

类型：`int`

返回窗口句柄

**示例**

```c
hwnd = op.GetForegroundFocus()
```

### GetForegroundWindow

获取顶层活动窗口,可以获取到按键自带插件无法获取到的句柄

```c
long GetForegroundWindow()
```

**返回值**

类型：`int`

返回窗口句柄

**示例**

```c
hwnd = op.GetForegroundWindow()
```

### GetMousePointWindow

获取鼠标指向的可见窗口句柄,可以获取到按键自带的插件无法获取到的句柄

```c
long GetMousePointWindow()
```

**返回值**

类型：`int`

返回窗口句柄

**示例**

```c
hwnd = op.GetMousePointWindow()
```

### GetPointWindow

获取给定坐标的可见窗口句柄

```c
long GetPointWindow(x,y)
```

| 参数 | 类型 | 描述        |
| ---- | ---- | ----------- |
| x    | int  | 屏幕 X 坐标 |
| y    | int  | 屏幕 Y 坐标 |

**返回值**

类型：`int`

返回窗口句柄

**示例**

```c
hwnd = op.GetPointWindow(100,100)
```

### GetProcessInfo

根据指定的 pid 获取进程详细信息,(进程名,进程全路径,CPU 占用率(百分比),内存占用量(字节))

```c
string GetProcessInfo(pid)
```

| 参数 | 类型 | 描述     |
| ---- | ---- | -------- |
| pid  | int  | 进程 pid |

**返回值**

类型：`string`

返回格式"进程名|进程路径|cpu|内存"

**示例**

```c
infos = op.GetProcessInfo(12345)
infos = split(infos,"|")
TracePrint "进程名:"&infos(0)
TracePrint "进程路径:"&infos(1)
TracePrint "进程CPU占用率(百分比):"&infos(2)
TracePrint "进程内存占用量(字节):"&infos(3)
```

### GetSpecialWindow

获取特殊窗口

```c
long GetSpecialWindow(flag)
```

| 参数 | 类型 | 描述     |
| ---- | ---- | -------- |
| flag | int  | 取值如下 |

**flag**

| 值  | 描述           |
| --- | -------------- |
| 0   | 获取桌面窗口   |
| 1   | 获取任务栏窗口 |

**返回值**

类型：`int`

返回窗口句柄

**示例**

```c
desk_win = op.GetSpecialWindow(0)
```

### GetWindow

获取给定窗口相关的窗口句柄

```c
long GetWindow(hwnd,flag)
```

| 参数 | 类型 | 描述           |
| ---- | ---- | -------------- |
| hwnd | int  | 指定的窗口句柄 |
| flag | int  | 取值如下       |

**flag**

| 值  | 描述               |
| --- | ------------------ |
| 0   | 获取父窗口         |
| 1   | 获取第一个儿子窗口 |
| 2   | 获取 First 窗口    |
| 3   | 获取 Last 窗口     |
| 4   | 获取下一个窗口     |
| 5   | 获取上一个窗口     |
| 6   | 获取拥有者窗口     |
| 7   | 获取顶层窗口       |

**返回值**

类型：`int`

返回窗口句柄

**示例**

```c
hwnd = op.GetWindow(hwnd,6)
```

### GetWindowClass

获取窗口的类名

```c
string GetWindowClass(hwnd)
```

| 参数 | 类型 | 描述           |
| ---- | ---- | -------------- |
| hwnd | int  | 指定的窗口句柄 |

**返回值**

类型：`string`

窗口的类名

**示例**

```c
class_name = op.GetWindowClass(hwnd)
```

### GetWindowProcessId

获取指定窗口所在的进程 ID

```c
long GetWindowProcessId(hwnd)
```

| 参数 | 类型 | 描述           |
| ---- | ---- | -------------- |
| hwnd | int  | 指定的窗口句柄 |

**返回值**

类型：`int`

返回进程 ID

**示例**

```c
process_id = op.GetWindowProcessId(hwnd)
```

### GetWindowProcessPath

获取指定窗口所在的进程的 exe 文件全路径

```c
string GetWindowProcessPath(hwnd)
```

| 参数 | 类型 | 描述           |
| ---- | ---- | -------------- |
| hwnd | int  | 指定的窗口句柄 |

**返回值**

类型：`string`

返回进程所在的全路径

**示例**

```c
process_path = op.GetWindowProcessPath(hwnd)
```

### GetWindowRect

获取窗口在屏幕上的位置

```c
long GetWindowRect(hwnd,x1,y1,x2,y2)
```

| 参数 | 类型  | 描述                            |
| ---- | ----- | ------------------------------- |
| hwnd | int   | 指定的窗口句柄                  |
| x1   | int\* | 变参指针: 返回窗口左上角 X 坐标 |
| y1   | int\* | 变参指针: 返回窗口左上角 Y 坐标 |
| x2   | int\* | 变参指针: 返回窗口右下角 X 坐标 |
| y2   | int\* | 变参指针: 返回窗口右下角 Y 坐标 |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op_ret = op.GetWindowRect(hwnd,x1,y1,x2,y2)
```

### GetWindowState

获取指定窗口的一些属性

```c
long GetWindowState(hwnd,flag)
```

| 参数 | 类型 | 描述           |
| ---- | ---- | -------------- |
| hwnd | int  | 指定的窗口句柄 |
| flag | int  | 取值如下       |

**flag**

| 值  | 描述                           |
| --- | ------------------------------ |
| 0   | 判断窗口是否存在               |
| 1   | 判断窗口是否处于激活           |
| 2   | 判断窗口是否可见               |
| 3   | 判断窗口是否最小化             |
| 4   | 判断窗口是否最大化             |
| 5   | 判断窗口是否置顶               |
| 6   | 判断窗口是否无响应             |
| 7   | 判断窗口是否可用(灰色为不可用) |

**返回值**

类型：`int`

- 0: 不满足条件
- 1: 满足条件

**示例**

```c
op_ret = op.GetWindowState(hwnd,3)
if op_ret ==1 {
  println("窗口已经最小化了")
}
```

### GetWindowTitle

获取窗口的标题

```c
string GetWindowTitle(hwnd)
```

| 参数 | 类型 | 描述           |
| ---- | ---- | -------------- |
| hwnd | int  | 指定的窗口句柄 |

**返回值**

类型：`string`

返回窗口的标题

**示例**

```c
title = op.GetWindowTitle(hwnd)
```

### MoveWindow

移动指定窗口到指定位置

```c
long MoveWindow(hwnd,x,y)
```

| 参数 | 类型 | 描述           |
| ---- | ---- | -------------- |
| hwnd | int  | 指定的窗口句柄 |
| x    | int  | 指定的 X 坐标  |
| y    | int  | 指定的 Y 坐标  |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op.MoveWindow(hwnd,100,200)
```

### ScreenToClient

把屏幕坐标转换为窗口坐标

```c
long ScreenToClient(hwnd,x,y)
```

| 参数 | 类型  | 描述                  |
| ---- | ----- | --------------------- |
| hwnd | int   | 指定的窗口句柄        |
| x    | int\* | 变参指针: 屏幕 X 坐标 |
| y    | int\* | 变参指针: 屏幕 Y 坐标 |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
var x =100
var y =100
op_ret = op.ScreenToClient(hwnd,&x,&y)
```

### SetClientSize

设置窗口客户区域的宽度和高度

```c
long SetClientSize(hwnd,width,height)

```

| 参数   | 类型 | 描述           |
| ------ | ---- | -------------- |
| hwnd   | int  | 指定的窗口句柄 |
| width  | int  | 宽度           |
| height | int  | 高度           |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op_ret = op.SetClientSize(hwnd,800,600)
```

### SetWindowState

设置窗口的状态

```c
long SetWindowState(hwnd,flag)

```

| 参数 | 类型 | 描述           |
| ---- | ---- | -------------- |
| hwnd | int  | 指定的窗口句柄 |
| flag | int  | 取值定义如下   |

**flag**

| 值  | 描述                                         |
| --- | -------------------------------------------- |
| 0   | 关闭指定窗口                                 |
| 1   | 激活指定窗口                                 |
| 2   | 最小化指定窗口,但不激活                      |
| 3   | 最小化指定窗口,并释放内存,但同时也会激活窗口 |
| 4   | 最大化指定窗口,同时激活窗口                  |
| 5   | 恢复指定窗口 ,但不激活                       |
| 6   | 隐藏指定窗口                                 |
| 7   | 显示指定窗口                                 |
| 8   | 置顶指定窗口                                 |
| 9   | 取消置顶指定窗口                             |
| 10  | 禁止指定窗口                                 |
| 11  | 取消禁止指定窗口                             |
| 12  | 恢复并激活指定窗口                           |
| 13  | 强制结束窗口所在进程                         |
| 14  | 闪烁指定的窗口                               |
| 15  | 使指定的窗口获取输入焦点                     |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op_ret = op.SetWindowState(hwnd,0)
```

### SetWindowSize

设置窗口客户区域的宽度和高度

```c
long SetWindowSize(hwnd,width,height)
```

| 参数   | 类型 | 描述           |
| ------ | ---- | -------------- |
| hwnd   | int  | 指定的窗口句柄 |
| width  | int  | 宽度           |
| height | int  | 高度           |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op_ret = op.SetWindowSize(hwnd,300,400)
```

### SetWindowText

设置窗口的标题

```c
long SetWindowText(hwnd,title)
```

| 参数  | 类型   | 描述           |
| ----- | ------ | -------------- |
| hwnd  | int    | 指定的窗口句柄 |
| title | string | 标题           |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op_ret = op.SetWindowText(hwnd,"test")
```

### SetWindowTransparent

设置窗口的透明度

```c
long SetWindowTransparent(hwnd,trans)
```

| 参数  | 类型 | 描述                                                                         |
| ----- | ---- | ---------------------------------------------------------------------------- |
| hwnd  | int  | 指定的窗口句柄                                                               |
| trans | int  | 透明度取值(0-255) 越小透明度越大 0 为完全透明(不可见) 255 为完全显示(不透明) |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op_ret = op.SetWindowTransparent(hwnd,200)
```

### SendString

向指定窗口发送文本数据

```c
long SendString(hwnd,str)
```

| 参数 | 类型   | 描述           |
| ---- | ------ | -------------- |
| hwnd | int    | 指定的窗口句柄 |
| str  | string | 发送的文本数据 |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op_ret = op.SendString(hwnd,"我是来测试的")
```

### SendStringIme

向指定窗口发送文本数据-输入法

```c
long SendStringIme(hwnd,str)
```

| 参数 | 类型   | 描述           |
| ---- | ------ | -------------- |
| hwnd | int    | 指定的窗口句柄 |
| str  | string | 发送的文本数据 |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op_ret = op.SendStringIme(hwnd,"我是来测试的")
```

### RunApp

运行可执行文件,可指定模式

```c
long RunApp(app_path,mode)
```

| 参数     | 类型   | 描述                   |
| -------- | ------ | ---------------------- |
| app_path | string | 指定的可执行程序全路径 |
| mode     | int    | 取值如下               |

**mode**

| 值  | 描述     |
| --- | -------- |
| 0   | 普通模式 |
| 1   | 加强模式 |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op.RunApp("c:\\windows\\notepad.exe",0)
```

### WinExec

运行可执行文件，可指定显示模式

```c
long WinExec(cmdline, cmdshow)
```

| 参数    | 类型   | 描述                   |
| ------- | ------ | ---------------------- |
| cmdline | string | 指定的可执行程序全路径 |
| cmdshow | int    | 取值如下               |

**cmdshow**

| 值  | 描述                        |
| --- | --------------------------- |
| 0   | 隐藏                        |
| 1   | 用最近的大小和位置显示,激活 |

**返回值**

类型：`int`

- 0: 成功
- 1: 失败

**示例**

```c
op.WinExec("c:\\windows\\notepad.exe",1)
```

### GetCmdStr

运行命令行并返回结果

```c
string GetCmdStr(cmdline, millseconds)
```

| 参数        | 类型   | 描述                   |
| ----------- | ------ | ---------------------- |
| cmdline     | string | 指定的可执行程序全路径 |
| millseconds | int    | 等待的时间(毫秒)       |

**返回值**

类型：`string`

cmd 输出的字符

**示例**

```c
str = op.GetCmdStr("cmd.exe" 2000)
```
