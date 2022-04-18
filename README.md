# 自动每日健康打卡程序

## 更新内容

1. 将认证和打卡模块分离
2. 打卡增加新的项目“是否离宁”和“核酸时间”
3. 增加OCR识别验证码

## 安装

该项目依赖于一些python包，在使用前请务必保证这些包已经被正常安装

```bash
pip install -r requirements.txt
```

## 使用

### 直接传入用户名密码

在bash中执行

```bash
python main.py --username=<username> --password=<password>
```

其中上面的<code>\<username\></code>处填写用户名（学号/工号），例如DZ20000001，其中的<code>\<password\></code>处填写统一身份认证平台的密码。

### 通过文件传入密码

新建passwd.txt文件，按照以下格式填入用户名和密码

```bash
username:password
```

保存好文件后在bash中执行

```bash
python main.py --file=/path/to/passwd.txt
```

例如在当前目录下

```bash
python main.py --file=./passwd.txt
```

### 使用base64加密密码

如果你不想将密码明文直接传入程序，在运行参数中加上<code>--b64</code>，将password改为密码的base64密文即可，该参数对于统一身份认证平台的密码和邮件的密码一样生效。例如

```bash
python main.py --file=./passwd.txt --b64
```

或者

```bash
python main.py --username=<username> --password=<password> --b64
```

### 邮件通知

如果你希望在打卡成功后通过邮件通知，加上--mail_notify, --mail_user, --mail_pass, --mail_host四个参数，（经过测试对于拉姆达邮箱无需修改--mail_host参数，使用默认参数即可），例如

```bash
python main.py --username=<username> \
--password=<password> \
--b64 \
--mail_notify \
--mail_user <example@xxxxx.xxx.edu.cn> \
--mail_pass <your_email_password_base64>
```

### 强制打卡（调试用）

默认情况下如果打卡已经完成程序会取消打卡，如果添加<code>--force</code>参数则将覆盖上次打卡，并强制重新打卡。

### 添加任务计划

#### linux

在linux平台下，可以编辑<code>/etc/crontab</code>文件，并添加行

```bash
0 22 * * * <user> /path/to/your/python /path/to/main.py --file=/path/to/passwd.txt
30 22 * * * <user> /path/to/your/python /path/to/main.py --file=/path/to/passwd.txt #可以加多几个防止出现网络故障
```

#### 其他平台

（待更新）

## 承诺&&免责声明

### 请放心使用

该程序**不会访问**除了校园网以外的所有资源，**不会收集**任何与用户账号相关的信息，请各位用户放心使用，不放心的用户可以自行阅读程序源码。

### 免责声明

该程序仅为大家提供便利，如果因故离校或者出现任何健康状况请如实上报，因使用该程序导致的后果作者概不负责。
