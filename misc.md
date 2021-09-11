# 杂项wp

## 简单题目

### embarrass34

直接strings,grep时候记得要加-i忽略大小写

```
$ strings misc_02.pcapng  | grep -i flag
GET /flag.php HTTP/1.1
GET /flag.doc HTTP/1.1
flag{Good_b0y_W3ll_Done}
flag{Good_b0y_W3ll_Done
```

### 神奇的Modbus

wireshark中搜索字符串sctf,注意选择分组字节流并且不区分大小写,宽窄或者宽,因为有很多间隔0用strings看不出来.

```
PVÀ)#|EY|@@8«À¨À¨öó«#dÆýÿFPåÉj+(sctf{Easy_Mdbus}
```

### something_in_image

```
$ strings badimages | grep -i flag | tail
Flag.txt
Flag.txt
Flag.txt
Flag.txt
/mnt/test/Flag.txt
Flag{}
Flag{yc4pl0fvjs2k1t7T}
/mnt/test/Flag.txt
Flag{}
Flag{yc4pl0fvjs2k1t7T}
```

### wireshark-1

```
$ strings dianli_jbctf_MISC_T10075_20150707_wireshark.pcap  | grep -i password
email=flag&password=ffb7567a1d4f4abdffdb54e022f8facd&captcha=BYUG
```

### pure_color

StegSolve打开即可.一直翻到有图像那页.

flag{true_steganographers_doesnt_need_any_tools}



### Aesop_secret

用StegSolve拆分并拼图后得到密码ISCC.

strings得到AES密文:
U2FsdGVkX19QwGkcgD0fTjZxgijRzQOGbCWALh4sRDec2w6xsY/ux53Vuj/AMZBDJ87qyZL5kAf1fmAH4Oe13Iu435bfRBuZgHpnRjTBn5+xsDHONiR3t0+Oa8yG/tOKJMNUauedvMyN4v4QKiFunw==

cyberchef比较复杂比较全,其它网站有比较简单的解密.

<https://tool.oschina.net/encrypt/>,可离线保存在密码学工具中.

### 倒立屋

```
$ zsteg  倒立屋.png
imagedata           .. text: "\t\t\t\r\r\r\r\r\r"
b1,rgb,lsb,xy       .. text: "IsCc_2019"
b2,r,msb,xy         .. text: "t^y\t_{!iO"
b2,g,msb,xy         .. text: "UUUUUU`\rUUUU"
```

要倒着写flag...

### a_good_idea

binwalk出来后的两个文件要对比.但不是用stegslove的对比,而是用容差分析.
可以用compare或者用beyond compare 4对比两个文件进行容差分析,都能得到二维码图片.

$ compare to.png to_do.png  -compose src flag.png

