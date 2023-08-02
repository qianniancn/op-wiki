# op

op.opsoft

## 接口目录

- [Ver](#ver): 插件版本号
- [SetPath](#setpath): 设置全局路径
- [GetPath](#getpath): 获取全局路径
- [GetBasePath](#getbasepath): 获取插件所在目录
- [GetID](#getid): 获取对象 ID
- [GetLastError](#getlasterror): 获取最后的错误
- [SetShowErrorMsg](#setshowerrormsg): 设置是否弹出错误信息
- [Sleep](#sleep): 休眠
- [InjectDll](#injectdll): 注入 DLL
- [EnablePicCache](#enablepiccache): 是否启用图片缓存机制
- [CapturePre](#capturepre): 取上次操作的图色区域
- [SetScreenDataMode](#setscreendatamode): 设置屏幕数据模式

## 接口方法

### Ver

获取当前 op 插件的版本号

```c
string Ver()
```

**返回值**

类型：`string`

返回 op 插件的版本号

### SetPath

设置全局路径,设置了此路径后,所有接口调用中,相关的文件都相对于此路径. 比如图片,字库等.

```c
long SetPath(path)
```

| 参数 | 类型   | 描述         |
| ---- | ------ | ------------ |
| path | string | 指定的路径。 |

**返回值**

类型：`int`

- 0：表示操作成功。
- 1：表示操作失败。

**示例**

无

### GetPath

获取全局路径

```c
string GetPath()
```

**返回值**

类型：`string`

返回当前设置的全局路径

**示例**

无

### GetBasePath

获取插件目录

```c
string GetBasePath()
```

**返回值**

类型：`string`

返回当前插件所在路径

**示例**

无

### GetID

返回当前对象的 ID 值，这个值对于每个对象是唯一存在的。可以用来判定两个对象是否一致

```c
long GetID()
```

**返回值**

类型：`int`

当前对象的 ID 值.

**示例**

无

### GetLastError

获取最后的错误

```c
long GetLastError()
```

**返回值**

类型：`int`

- 0:表示无错误

**示例**

无

### SetShowErrorMsg

设置是否弹出错误信息,默认是打开

```c
long SetShowErrorMsg(show)
```

| 参数 | 类型 | 描述                                                  |
| ---- | ---- | ----------------------------------------------------- |
| show | int  | 0:关闭，1:显示为信息框，2:保存到文件,3:输出到标准输出 |

**返回值**

类型：`int`

- 0：表示操作成功。
- 1：表示操作失败。

**示例**

无

### Sleep

设置休眠时间

```c
long Sleep(millisecond)
```

| 参数        | 类型 | 描述           |
| ----------- | ---- | -------------- |
| millisecond | int  | 休眠时间(毫秒) |

**返回值**

类型：`int`

- 0：表示操作成功。
- 1：表示操作失败。

**示例**

无

### InjectDll

将指定的 DLL 注入到指定的进程中

```c
void InjectDll(const wchar_t* process_name,const wchar_t* dll_name, long* ret);
```

| 参数         | 类型   | 描述                      |
| ------------ | ------ | ------------------------- |
| process_name | string | 指定要注入 DLL 的进程名称 |
| dll_name     | string | 注入的 DLL 名称           |

**返回值**

类型：`int`

- 0：表示操作成功。
- 1：表示操作失败。

**示例**

无

### EnablePicCache

设置是否开启或者关闭插件内部的图片缓存机制

```c
long EnablePicCache(enable)
```

| 参数   | 类型 | 描述           |
| ------ | ---- | -------------- |
| enable | int  | 0：关闭,1:打开 |

**返回值**

类型：`int`

- 0：表示操作成功。
- 1：表示操作失败。

**示例**

无

### CapturePre

取上次操作的图色区域，保存为 file(24 位位图)

```c
long CapturePre(file)
```

| 参数 | 类型   | 描述                                                           |
| ---- | ------ | -------------------------------------------------------------- |
| file | string | 设置保存文件名,保存路径是 SetPath 设置的目录，也可以指定全路径 |

**返回值**

类型：`int`

- 0：表示操作成功。
- 1：表示操作失败。

**示例**

```
op.CapturePre("screen.bmp")
```

### SetScreenDataMode

设置屏幕数据模式

```c
long SetScreenDataMode(mode)
```

| 参数 | 类型 | 描述                        |
| ---- | ---- | --------------------------- |
| mode | int  | 0:从上到下(默认),1:从下到上 |

**返回值**

类型：`int`

- 0：表示操作成功。
- 1：表示操作失败。

**示例**

无
