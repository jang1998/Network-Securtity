# Upload-labs

1. 前端：复制网页源代码，在html中删去脚本，添加action到发送文件处

2. MIME绕过：看代码是依据content-type判断文件   抓包改content-type为image/jpeg

3. 特殊解析后缀：看代码是依据文件后缀名判断，黑名单验证，不过不够严谨，php5在apache也可以解析成php，上传php5后缀即可

4. .htaccess解析：后缀名全屏蔽，通过中间件apache解析漏洞。上传.htaccess文件将jpg文件解析成php

5. ini脚本绕过：

6. 大小写绕过：无小写转换，通过大小写混合上传

7. 空格绕过：上传时抓包，在文件名后加空格，系统存储文件会自动删除末尾空格[0x20]

8. 点绕过：上传时抓包，在文件名后加 . ，系统存储文件会自动删除末尾. 

9. ::$$DATA绕过：上传时抓包，在文件名后加::$$DATA，系统识别为文件流会忽略末尾 

10. 一次过滤绕过：后端没有对文件名进行多次过滤，可以抓包将后缀改为1.php.空格.或任意多个点与空格组合

11. 双后缀名绕过：后端没有对文件名进行多次过滤，可以抓包将后缀改为1.pphphp

12. %00绕过(有apache版本要求)：Get提交地址，%00截断，后续不再读取，抓包文件头保存处修改为../upload/1.php%00   

13. %00绕过(有apache版本要求)：POST提交地址，%00截断，后续不再读取，抓包文件保存处修改为../upload/1.php%00   （此处%00要url解码，因为post不会自动编码或解码，提交后任何内容都认为是原内容）

14. 文件头检测：16进制打开，更改文件头，绕过(要配合文件包含漏洞)

15. getimagesize：获取图片信息，若不是图片则返回为空(要配合文件包含漏洞)

16. 突破exif__imagetype：只接受图片，上传正常图(要配合文件包含漏洞)

17. 二次渲染+条件竞争：图片上传上去后能在网站进行二次更改，涉及逻辑漏洞，如果验证是在上传之后，那么在上传的同时已经把图片保存服务器，所以可以不断访问该文件，占用不让服务器能删除文件

18. 条件竞争

19. 1

20. /.绕过：文件支持自命名，在上传时候抓包修改为/upload/1.php/.   系统认为该地址是文件

21. 字符串绕过：通过自定义字符串save_name[0]与save_name[2]绕过验证上传图片

    ![image-20210427221855098](C:\Users\Jang\AppData\Roaming\Typora\typora-user-images\image-20210427221855098.png)

