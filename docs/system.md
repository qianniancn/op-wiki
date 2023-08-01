# system

命令

## 接口目录

- [RunApp](#runapp): 运行可执行文
- [WinExec](#winexec): 运行可执行文件
- [GetCmdStr](#getcmdstr): 运行命令行

## 接口方法

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
