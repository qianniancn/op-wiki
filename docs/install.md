# 安装

## 下载

插件和配套工具可在这里获得 [Github](https://github.com/WallBreaker2/op/releases)

## 注册

### 注册

把注册插件到系统

把下载下来的插件解压后，选中文件目录中的：`install.bat`右击**以管理员的身份运行**

手动使用 cmd 命令行进行注册

```cmd
cd /d op路径
regsvr32 op_x86.dll
```

### 免注册

在插件目录中找到 tool.dll 和 tools_64.dll 文件, 此文件导出 2 函数

`setupA`: A 表示 ANSI 字符集,使用 ANSI 字符编码

`setupW`: W 表示宽字符集,使用 Unicode 字符编码

| 参数 | 类型   | 描述                 |
| ---- | ------ | -------------------- |
| path | string | 指定 op.dll 的路径。 |

**返回值**

类型：`int`

- 0：表示操作失败。
- 1：表示操作成功。

**示例**

```c
int result = setupW(L"./op_x64.dll");
if (result == 0) {
    printf("加载 op_x64 文件失败！");
} else {
    printf("加载 op_x64文件成功！");
}
```
