# 一、简介

*pdf2htmlEX*是一个pdf转html的开源软件,效果非常理想。可以准确的将复杂的学术类pdf转成html，同时保留源文件中的格式。

源码地址(已停止维护)
https://github.com/coolwanglu/pdf2htmlEX

# 二、下载与安装

到如下地址下载windows系统绿色版可执行文件：
http://soft.rubypdf.com/software/pdf2htmlex-windows-version

# 三、使用

下载后解压，将要处理的pdf也放到pdf2htmlEX.exe所在的目录。

然后运行如下命令：

```bat
pdf2htmlex input.pdf
```

执行完毕后，会在同目录下生成与pdf同名的单页面html文件(字体和图片都会以base64编码嵌入)

直接运行可查看帮助：

    pdf2htmlex

# 四、备注

## 1. 显示中文乱码

生成的html文件中

第22行，以“@font-face{font-family:ff1;src:url('data:application/font-woff;base64”开头的内容对应加粗字体

第23行，以“@font-face{font-family:ff2;src:url('data:application/font-woff;base64”开头的内容对应正常字体


## 2. pdf转excel

Acrobat自带的转换功能就已经够好了。
   
