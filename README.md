# oracle_arm
oracle arm registration script. 乌龟壳刷ARM脚本

# 本脚本优点

简单,主机配置好oci，然后下载main.tf即可，不用自己获取各种参数。
## 运行环境配置
本简单脚本使用python3编写，请自行配置好python3环境和requests库。（高版本的linux默认都自己带了,啥也不用装，可以要装一下git）

比如检查本机的环境：

终端运行 `python3` 进入python交互环境，如果 `import requests`没有报错，那就ok了
# 配置oci

## 安装oci

```shell
bash -c "$(curl –L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
```
一路会车 然后 `exec -l $SHELL`重启shell 

使用 `oci -v`命令可以查看是否安装成功

## 配置oci

参考[大鸟博客](https://www.daniao.org/14035.html)中的 **3、复制租户和用户的ocid** 和 **4、配置cli** 配置好oci和公钥 

# 下载main.tf

参考[大鸟博客-Oracle甲骨文 ARM VPS自动抢购脚本 – 利用宝塔面板+oci](https://www.daniao.org/14121.html) 中的 **1、生成main.tf** 即可，下载到本地并解压出main.tf文件

# 脚本需要改的地方
## 启动 tg推送

修改
```python
USE_TG = False  # 如果启用tg推送 要设置为True
TG_BOT_TOKEN = ''  # 通过 @BotFather 申请获得，示例：1077xxx4424:AAFjv0FcqxxxxxxgEMGfi22B4yh15R5uw
TG_USER_ID = ''  # 用户、群组或频道 ID，示例：129xxx206
```
USE_TG=True
其他的token和id自行配置自己的

## 修改硬盘大小
默认是50G，
修改`HARDDRIVE_SIZE = 50` 为想要的大小，不过可能oci创建的时候不会成功，默认50就行，创建成功后后台可以改

# 运行脚本

```
git clone https://github.com/n0thing2speak/oracle_arm

cd oracle_arm
```
上传 `main.tf` 文件到 oracle_arm 目录

首先运行一遍测试一下
`python3 oracle_arm.py main.tf` 
稍等一下看返回结果，一般是500就对了，慢不是程序的问题，是oci的返回本身就慢，可能需要30s到2分钟一次

最后运行

`nohup python3 oracle_arm.py main.tf >> /dev/null 2>&1 &`

会自动停止的,不用管了。Done and enjoy 🎉

# 再次感谢

[大鸟博客](https://www.daniao.org/) 最先公布出刷arm方法，本脚本只是简化了一些步骤。

