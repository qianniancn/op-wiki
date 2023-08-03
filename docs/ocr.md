# OCR

文字识别

## 接口目录

- [SetOcrEngine](#setocrengine): 设置 OCR 引擎 **未导出 COM**
- [SetDict](#setdict): 设置字库
- [SetMemDict](#setmemdict): 设置内存字库
- [UseDict](#usedict): 选择字库
- [Ocr](#ocr): 文字识别
- [OcrEx](#ocrex): 文字识别返回坐标
- [OcrAuto](#ocrauto): 文字识别自动二值化
- [OcrFromFile](#ocrfromfile): 从文件识别文字
- [OcrAutoFromFile](#ocrautofromfile): 从文件识别文字
- [FindStr](#findstr): 寻找文字
- [FindStrEx](#findstrex): 寻找文字
- [FindLine](#findline): 寻找屏幕中的线

## 接口方法

### SetOcrEngine

设置 OCR 引擎

```c
long SetOcrEngine(path_of_engine,dll_name,argv)
```

| 参数           | 类型   | 描述                                            |
| -------------- | ------ | ----------------------------------------------- |
| path_of_engine | string | 指定 OCR 引擎的路径                             |
| dll_name       | string | OCR 引擎 DLL 名称                               |
| argv           | string | 指定要传递给 OCR 引擎的任何其他参数,可以为 NULL |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

无

### SetDict

设置字库文件(index：范围:0-9)不能超过 10 个字库

```c
long SetDict(index,file)
```

| 参数  | 类型   | 描述                  |
| ----- | ------ | --------------------- |
| index | int    | 字库的序号,取值为 0-9 |
| file  | string | 字库文件名            |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

```c
op_ret = op.SetDict(0,"test.txt")
```

注: 此函数速度很慢，全局初始化时调用一次即可，切换字库用 UseDict

### SetMemDict

设置内存字库文件

```c
void SetMemDict(long idx, const wchar_t* data, long size, long* ret);
```

| 参数  | 类型   | 描述         |
| ----- | ------ | ------------ |
| index | int    | 字库的序号   |
| data  | string | 字库内容数据 |
| size  | int    | 字库大小     |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

无

### UseDict

选择使用哪个字库文件进行识别(index：范围:0-9)

```c
long UseDict(index)
```

| 参数  | 类型 | 描述       |
| ----- | ---- | ---------- |
| index | int  | 字库的序号 |

**返回值**

类型：`int`

- 0：失败
- 1：成功

**示例**

```c
op_ret = op.UseDict(1)
ss = op.Ocr(0,0,2000,2000,"FFFFFF-000000",1.0)
op_ret = op.UseDict(0)
long UseDict(index)
```

### Ocr

识别屏幕范围(x1,y1,x2,y2)内符合 color_format 的字符串

若当前对象未设置字库，则使用 ocr 引擎进行文字识别

```c
string Ocr(x1,y1,x2,y2,color_format,sim)
```

| 参数         | 类型   | 描述                                                             |
| ------------ | ------ | ---------------------------------------------------------------- |
| x1           | int    | 区域的左上 X 坐标                                                |
| y1           | int    | 区域的左上 Y 坐标                                                |
| x2           | int    | 区域的右下 X 坐标                                                |
| y2           | int    | 区域的右下 Y 坐标                                                |
| color_format | string | 颜色格式串，比如"FFFFFF-000000\|CCCCCC-000000"每种颜色用"\|"分割 |
| sim          | double | 相似度,取值范围 0.1-1.0                                          |

**返回值**

类型：`string`

返回识别到的字符串

**示例**

```c
//RGB单色识别
s = op.Ocr(0,0,2000,2000,"9f2e3f-000000",1.0)
println(s)

//RGB单色差色识别
s = op.Ocr(0,0,2000,2000,"9f2e3f-030303",1.0)
println(s)

//RGB多色识别(最多支持10种,每种颜色用"|"分割)
s = op.Ocr(0,0,2000,2000,"9f2e3f-030303|2d3f2f-000000|3f9e4d-100000",1.0)
println(s)
```

### OcrEx

该方法可以返回识别到的字符串，以及每个字符的坐标

若当前对象未设置字库，则使用 ocr 引擎进行文字识别

```c
string OcrEx(x1,y1,x2,y2,color_format,sim)
```

| 参数         | 类型   | 描述                                                             |
| ------------ | ------ | ---------------------------------------------------------------- |
| x1           | int    | 区域的左上 X 坐标                                                |
| y1           | int    | 区域的左上 Y 坐标                                                |
| x2           | int    | 区域的右下 X 坐标                                                |
| y2           | int    | 区域的右下 Y 坐标                                                |
| color_format | string | 颜色格式串，比如"FFFFFF-000000\|CCCCCC-000000"每种颜色用"\|"分割 |
| sim          | double | 相似度,取值范围 0.1-1.0                                          |

**返回值**

类型：`string`

返回识别到的字符串以及坐标

**示例**

和 Ocr 函数相同，只是结果处理有所不同 如下

```c
op_ret = op.OcrEx(0,0,2000,2000,"ffffff|000000",1.0)
ss = split(op_ret,"|")
index = 0
count = UBound(ss) + 1
Do While index < count
   TracePrint ss(index)
   sss = split(ss(index),"$")
   ocr_s = int(sss(0))
   x = int(sss(1))
   y = int(sss(2))
   TracePrint ocr_s & ","&x&","&y
   index = index+1
Loop
```

### OcrAuto

识别屏幕范围(x1,y1,x2,y2)内的字符串,自动二值化，而无需指定颜色

适用于字体颜色和背景相差较大的场合

```c
string OcrAuto(x1,y1,x2,y2,sim)
```

| 参数 | 类型   | 描述                    |
| ---- | ------ | ----------------------- |
| x1   | int    | 区域的左上 X 坐标       |
| y1   | int    | 区域的左上 Y 坐标       |
| x2   | int    | 区域的右下 X 坐标       |
| y2   | int    | 区域的右下 Y 坐标       |
| sim  | double | 相似度,取值范围 0.1-1.0 |

**返回值**

类型：`string`

返回识别到的字符串

**示例**

```c
s = op.OcrAuto(0,0,100,200,1.0)
println(s)
```

### OcrFromFile

从文件中识别图片

```c
string OcrFromFile(file_name,color_format,sim)
```

| 参数         | 类型   | 描述                    |
| ------------ | ------ | ----------------------- |
| file_name    | string | 文件名                  |
| color_format | string | 颜色格式串              |
| sim          | double | 相似度,取值范围 0.1-1.0 |

**返回值**

类型：`string`

返回识别到的字符串

**示例**

```c
//RGB单色识别
s = op.OcrFromFile("test.png","9f2e3f-000000",1.0)
println(s)
```

### OcrAutoFromFile

从文件中识别图片,自动二值化,无需指定颜色

```c
string OcrAutoFromFile(file_name,sim)
```

| 参数      | 类型   | 描述                    |
| --------- | ------ | ----------------------- |
| file_name | string | 文件名                  |
| sim       | double | 相似度,取值范围 0.1-1.0 |

**返回值**

类型：`string`

返回识别到的字符串

**示例**

```c
//RGB单色识别
s = op.OcrAutoFromFile("test.png",1.0)
println(s)
```

### FindStr

在屏幕范围(x1,y1,x2,y2)内,查找 string(可以是任意个字符串的组合),并返回符合 color_format 的坐标位置

```c
long FindStr(x1,y1,x2,y2,string,color_format,sim,intX,intY)
```

| 参数         | 类型   | 描述                                                                       |
| ------------ | ------ | -------------------------------------------------------------------------- |
| x1           | int    | 区域的左上 X 坐标                                                          |
| y1           | int    | 区域的左上 Y 坐标                                                          |
| x2           | int    | 区域的右下 X 坐标                                                          |
| y2           | int    | 区域的右下 Y 坐标                                                          |
| string       | string | 待查找的字符串,可以是字符串组合，比如"长安\|洛阳\|大雁塔",中间用"\|"来分割 |
| color_format | string | 颜色格式串，比如"FFFFFF-000000\|CCCCCC-000000"每种颜色用"\|"分割           |
| sim          | double | 相似度,取值范围 0.1-1.0                                                    |
| intX         | int\*  | 变参指针: 返回 X 坐标没找到返回-1                                          |
| intY         | int\*  | 变参指针: 返回 Y 坐标没找到返回-1                                          |

**返回值**

类型：`int`

返回字符串的索引 没找到返回-1, 比如"长安|洛阳",若找到长安，则返回 0

**示例**

此函数的原理是先 Ocr 识别，然后再查找,若当前对象未设置字库，则使用 ocr 引擎进行文字识别

```c
op_ret = op.FindStr(0,0,2000,2000,"长安","9f2e3f-000000",1.0,intX,intY)
If intX >= 0 and intY >= 0 Then
     op.MoveTo intX,intY
End If



op_ret = op.FindStr(0,0,2000,2000,"长安|洛阳","9f2e3f-000000",1.0,intX,intY)
If intX >= 0 and intY >= 0 Then
     op.MoveTo intX,intY
End If

// 查找时,对多行文本进行换行,换行分隔符是"|". 语法是在","后增加换行字符串.任意字符串都可以.
op_ret = op.FindStr(0,0,2000,2000,"长安|洛阳","9f2e3f-000000,|",1.0,intX,intY)
If intX >= 0 and intY >= 0 Then
     op.MoveTo intX,intY
End If
```

### FindStrEx

在屏幕范围(x1,y1,x2,y2)内,查找 string(可以是任意字符串的组合)

该接口和 FindStr 类似，可以返回符合 color_format 的所有坐标位置

```c
string FindStrEx(x1,y1,x2,y2,string,color_format,sim)
```

| 参数         | 类型   | 描述                                                                       |
| ------------ | ------ | -------------------------------------------------------------------------- |
| x1           | int    | 区域的左上 X 坐标                                                          |
| y1           | int    | 区域的左上 Y 坐标                                                          |
| x2           | int    | 区域的右下 X 坐标                                                          |
| y2           | int    | 区域的右下 Y 坐标                                                          |
| string       | string | 待查找的字符串,可以是字符串组合，比如"长安\|洛阳\|大雁塔",中间用"\|"来分割 |
| color_format | string | 颜色格式串，比如"FFFFFF-000000\|CCCCCC-000000"每种颜色用"\|"分割           |
| sim          | double | 相似度,取值范围 0.1-1.0                                                    |

**返回值**

类型：`string`

返回所有找到的坐标集合,格式如下: "id,x0,y0|id,x1,y1|......|id,xn,yn" 比如"0,100,20|2,30,40" 表示找到了两个,第一个,对应的是序号为 0 的字符串,坐标是(100,20),第二个是序号为 2 的字符串,坐标(30,40)

**示例**

此函数的原理是先 Ocr 识别，然后再查找,若当前对象未设置字库，则使用 ocr 引擎进行文字识别

```c
op_ret = op.FindStrEx(0,0,2000,2000,"长安|洛阳","9f2e3f-000000",1.0)
If len(op_ret) > 0 Then
   ss = split(op_ret,"|")
   index = 0
   count = UBound(ss) + 1
   Do While index < count
      TracePrint ss(index)
      sss = split(ss(index),",")
      id = int(sss(0))
      x = int(sss(1))
      y = int(sss(2))
      op.MoveTo x,y
      Delay 1000
      index = index+1
   Loop
End If
```

### FindStrEx

在屏幕范围(x1,y1,x2,y2)内,查找 string(可以是任意字符串的组合)

该接口和 FindStr 类似，可以返回符合 color_format 的所有坐标位置

```c
string FindStrEx(x1,y1,x2,y2,string,color_format,sim)
```

| 参数         | 类型   | 描述                                                                       |
| ------------ | ------ | -------------------------------------------------------------------------- |
| x1           | int    | 区域的左上 X 坐标                                                          |
| y1           | int    | 区域的左上 Y 坐标                                                          |
| x2           | int    | 区域的右下 X 坐标                                                          |
| y2           | int    | 区域的右下 Y 坐标                                                          |
| string       | string | 待查找的字符串,可以是字符串组合，比如"长安\|洛阳\|大雁塔",中间用"\|"来分割 |
| color_format | string | 颜色格式串，比如"FFFFFF-000000\|CCCCCC-000000"每种颜色用"\|"分割           |
| sim          | double | 相似度,取值范围 0.1-1.0                                                    |

**返回值**

类型：`string`

返回所有找到的坐标集合,格式如下: "id,x0,y0|id,x1,y1|......|id,xn,yn" 比如"0,100,20|2,30,40" 表示找到了两个,第一个,对应的是序号为 0 的字符串,坐标是(100,20),第二个是序号为 2 的字符串,坐标(30,40)

**示例**

此函数的原理是先 Ocr 识别，然后再查找,若当前对象未设置字库，则使用 ocr 引擎进行文字识别

```c
op_ret = op.FindStrEx(0,0,2000,2000,"长安|洛阳","9f2e3f-000000",1.0)
If len(op_ret) > 0 Then
   ss = split(op_ret,"|")
   index = 0
   count = UBound(ss) + 1
   Do While index < count
      TracePrint ss(index)
      sss = split(ss(index),",")
      id = int(sss(0))
      x = int(sss(1))
      y = int(sss(2))
      op.MoveTo x,y
      Delay 1000
      index = index+1
   Loop
End If
```

### FindLine

在指定的屏幕坐标范围内，查找指定颜色的直线

```c
string FindLine(x1,y1,x2,y2,color_format,sim)
```

| 参数         | 类型   | 描述                                                             |
| ------------ | ------ | ---------------------------------------------------------------- |
| x1           | int    | 区域的左上 X 坐标                                                |
| y1           | int    | 区域的左上 Y 坐标                                                |
| x2           | int    | 区域的右下 X 坐标                                                |
| y2           | int    | 区域的右下 Y 坐标                                                |
| color_format | string | 颜色格式串，比如"FFFFFF-000000\|CCCCCC-000000"每种颜色用"\|"分割 |
| sim          | double | 相似度,取值范围 0.1-1.0                                          |

**返回值**

类型：`string`

返回识别到的结果

**示例**

无
