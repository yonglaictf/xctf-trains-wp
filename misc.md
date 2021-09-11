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

### 2017_Dating_in_Singapore6

用出现的数字在日历pdf上画图得出字符...

### simple_transfer

foremost 流量包得到pdf,pdf用firefox打开得到:

HITB{b3d0e380e9c39352c667307d010775ca}

或者随便打开之后另存为文本都可以.

### Erik-Baleog-and-Olaf

在文件中得到原图地址,然后两个容差比较得到二维码.

### János-the-Ripper

暴力破解zip密码得到flag.

密码4位数.

可用ARCHPR也可以john.john用法如下:

```
nicroot@kaliwin:/mnt/f/trains/xctf/misc$ zip2john misc100.zip >> misc100pass
ver 2.0 misc100.zip/flag.txt PKZIP Encr: cmplen=39, decmplen=25, crc=7788D444
nicroot@kaliwin:/mnt/f/trains/xctf/misc$ john misc100pass
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 8 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 3 candidates buffered for the current salt, minimum 8 needed for performance.
Warning: Only 2 candidates buffered for the current salt, minimum 8 needed for performance.
Warning: Only 4 candidates buffered for the current salt, minimum 8 needed for performance.
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst, rules:Wordlist
fish             (misc100.zip/flag.txt)
1g 0:00:00:00 DONE 2/3 (2021-09-11 17:35) 16.66g/s 916283p/s 916283c/s 916283C/s 123456..faithfaith
Use the "--show" option to display all of the cracked passwords reliably
Session completed
nicroot@kaliwin:/mnt/f/trains/xctf/misc$ john misc100pass -show
misc100.zip/flag.txt:fish:flag.txt:misc100.zip::misc100.zip

1 password hash cracked, 0 left
```

### hit-the-core

strings后看到:cvqAeqacLtqazEigwiXobxrCrtuiTzahfFreqc{bnjrKwgk83kgd43j85ePgb_e_rwqr7fvbmHjklo3tews_hmkogooyf0vbnk0ii87Drfgh_n kiwutfb0ghk9ro987k5tfb_hjiouo087ptfcv}

比赛名:alexctf

间隔出现的flag.

```
>>> s="cvqAeqacLtqazEigwiXobxrCrtuiTzahfFreqc{bnjrKwgk83kgd43j85ePgb_e_rwqr7fvbmHjklo3tews_hmkogooyf0vbnk0ii87Drfgh_n kiwutfb0ghk9ro987k5tfb_hjiouo087ptfcv}"
>>> s[3::5]
'ALEXCTF{K33P_7H3_g00D_w0rk_up}'
>>>
```

### easycap

wireshark追踪流.