很多情况下，大家都会遇到一个问题，自己电脑上配置的SSH Key可以与自己的gitbub账号匹配，却不能匹配公司内部的git服务器账号，即gitlab。下面我将讲述这两种账号的配置过程：
**1. github账号SSH Key配置**
(1) 设置git的名字和邮箱，这点很重要，尤其是对于gitlab的配置

```
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"12
```

(2) 初始化git

```
git init
```

(3) 生成SSH Key

```
ssh-keygen -t rsa -C "你的github账号对应的邮箱"
```

可以看到结果如下，选择默认，passphrase可以根据自己的需要设置。
![这里写图片描述](https://img-blog.csdn.net/20170809165527708?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHV0aWFueW91MTIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

输入cat id_rsa.pub获取公钥：
![这里写图片描述](https://img-blog.csdn.net/20170809165730004?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHV0aWFueW91MTIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

(4)将公钥加入到github中，选择setting->SSH KEY添加即可。如下图：
![这里写图片描述](https://img-blog.csdn.net/20170809170015478?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHV0aWFueW91MTIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

记住，这里的pub文件叫做id_rsa.pub

**2. 配置gitlab SSH Key**
方法和上面类似，只是生成的Key需要这样输入：

```
ssh-keygen -t rsa -C "GitLib" -b 4096
1
```

这里取名为hty.pub。

**3. 配置两种不同的SSH key**
首先需要将密钥添加到SSH agent中，因为默认只读取id_rsa，为了让SSH识别新的私钥，需将其添加到SSH agent中：

```
ssh-add ~/.ssh/hty
1
```

如果出现Could not open a connection to your authentication agent的错误，就试着用以下命令：

```
ssh-agent bash
ssh-add ~/.ssh/hty12
```

找到.ssh的默认目录，一般在C:\Users\Administrator目录下，将git bash的工作目录切换到该目录，如下：

```
cd C:\Users\Administrator\.ssh
1
```

输入touch config, 创建config文件，内容如下：

```
Host github.com  
    HostName github.com  
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/id_rsa  

Host gitlab  
    HostName gitlab 
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/hty  123456789
```

**4. 验证是否正确**
(1) 针对github，输入指令：

```
ssh -T git@github.com
1
```

![这里写图片描述](https://img-blog.csdn.net/20170809171253164?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHV0aWFueW91MTIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

(2) 针对gitlab, 输入指令：

```
ssh -T git@gitlab
1
```

![这里写图片描述](https://img-blog.csdn.net/20170809171457248?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHV0aWFueW91MTIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

以上结果，表示配置成功。如果失败，请仔细阅读上述步骤，或者给我留言，谢谢！