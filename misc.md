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

### glance-50

在线工具拆分GIF然后在横排合成.<https://uutool.cn/gif2img/>和<https://merge.imageonline.co/cn/>

离线情况下,可以python编程或者用命令.

先把 gif 分解开，kali 的 convert 命令可以分解图片

```
convert glance.gif flag.png
```

-tile 是拼接时每行和每列的图片数，这里用 x1，就是只一行
-geometry 是首选每个图和边框尺寸，我们边框为 0，图照原始尺寸即可

```
montage flag*.png -tile x1 -geometry +0+0 flag.png 
```

但因为bash中排序是按照字符的.所以会有部分错位.

可以这样在convert的输出补0,然后也可以继续用convert合成:

```bash
convert 9266eadf353d4ada94ededaeb96d0c50.gif flag-%04d.png
convert +append *.png flag.png
```

### Ditf

宽高爆破后得到密码.

PNG爆破宽高脚本:

```python
# -*- coding: cp936 -*-
import binascii
import struct
import sys

file = input("图片地址：")
fr = open(file,'rb').read()
data = bytearray(fr[0x0c:0x1d])
crc32key = eval('0x'+str(binascii.b2a_hex(fr[0x1d:0x21]))[2:-1])
#原来的代码: crc32key = eval(str(fr[29:33]).replace('\\x','').replace("b'",'0x').replace("'",''))
n = 4095
for w in range(n):
    width = bytearray(struct.pack('>i', w))
    for h in range(n):
        height = bytearray(struct.pack('>i', h))
        for x in range(4):
            data[x+4] = width[x]
            data[x+8] = height[x]
        crc32result = binascii.crc32(data) & 0xffffffff
        if crc32result == crc32key:
            print(width,height)
            newpic = bytearray(fr)
            for x in range(4):
                newpic[x+16] = width[x]
                newpic[x+20] = height[x]
            fw = open(file+'.png','wb')
            fw.write(newpic)
            fw.close
            sys.exit()

```

密码解压后得到流量包.用wireshark提取所有文件后,在其中一个文件中找到base64编码过的flag.

```
$ cat * | grep -ai Zmx
  ZmxhZ3tPel80bmRfSGlyMF9sb3YzX0ZvcjN2ZXJ9
```

### easycap

wireshark追踪流.

### stage1

stegslove 切到其它通道看到二维码,解码后再按照HEX解码,得到:

```
.ó
¶&jWc............@...s
...d.....Z..d..S(....c............C...sN...d..d..d..d..d..d..d..d..g..}..d..}..x..|..D]..}..|..t..|.....7}..q+.W|..GHd..S(	...NiA...il...ip...ih...ia...iL...ib...t....(....t....chr(....t....strt....flagt....i(....(....s....test.pyR........s
.........
...N(....R....(....(....(....s....test.pyt....<module>....s....
```

看着像pyc代码,用uncompyle6反编译饿到flag.

```
$ uncompyle6 download.pyc
# uncompyle6 version 3.7.4
# Python bytecode 2.7 (62211)
# Decompiled from: Python 3.8.6 (default, Oct 19 2020, 10:44:56)
# [GCC 10.2.0]
# Embedded file name: test.py
# Compiled at: 2016-06-22 13:48:38


def flag():
    str = [
     65, 108, 112, 104, 97, 76, 97, 98]
    flag = ''
    for i in str:
        flag += chr(i)

    print flag
# okay decompiling download.pyc
```

### Miscellaneous-200

txt文件中是一堆RGB像素点.

```
$ head 62f4ea780ecf4e6bbef5f40d674ec073.txt
255,255,255
255,255,255
255,255,255
255,255,255
255,255,255
255,255,255
255,255,255
255,255,255
255,255,255
255,255,255
```

用cyberchef一把梭.

```
CyberChef_v9.32.3.html#recipe=Find_/_Replace(%7B'option':'Extended%20(%5C%5Cn,%20%5C%5Ct,%20%5C%5Cx...)','string':'%5C%5Cn'%7D,',',true,false,true,false)From_Decimal('Comma',false)Generate_Image('RGB',1,244)Flip_Image('Horizontal')&input=MTExMjIz
```

1.替换换行为逗号,2.From_Decimal,以逗号为分隔符,转换为bytes,3. 用RGB模式Generate_Image,每行244点.4.反转图像Flip_Image.

244个像素点是因为发现像素点为61时图像有规律.所以以其倍数尝试.也可观察一共61366个像素点,61为其中一个质数.

### Hear-with-your-Eyes

Audacity打开用频谱图查看即可看到flag.

用指数型频谱图更清楚.

### Hidden-Message

流量包中的两种端口号的变化分别是0和1.

### Recover-Deleted-File

使用命令:extundelete disk-image --restore-all

### What-is-this

容差.compare

### red_green

红绿代表01序列.

用cyberchef转为RGB逗号序列.再用python处理为两种字符序列.再用cyberchef转换为01序列(可能需要对换),然后FROM BINARY得到图像.

```python
with open('RGB.txt', 'rt') as f:
    data=f.read()
x = data.split(',')
print(len(x))
print(len(x)/3)

i = 0
out = ''
while i < len(x)/3:
     if x[3*i]=='255' and x[3*i+1]=='0' and x[3*i+2]=='0':
             out = out + 'A'
     else:
             out = out + 'B'
     i = i + 1

with open('somefile.txt', 'wt') as f:
     f.write(out)

```

### normal_png

CRC爆宽高.

### 就在其中

NetworkMiner挖出文件,然后解密.注意networkminer可能不支持的格式需要wireshark转换下.

openssl rsautl -decrypt  -inkey test.key -in key.txt

f9b3bfadac030a918780cd7a9ec7e1e7

### 再见李华

根据提示密码是LiHua结尾至少1000个字符也就是8以上.写脚本爆破md5,特别注意python的hashlib的md5中update是append的意思,不是更新.


```python
import hashlib
import string

m = hashlib.md5()

m.update(b'123')

md5target = '1a4fb3fb5ee123'
# md5target = '3498110ce6b4ed'

m.hexdigest().find(md5target)
trysnum = 0
for i in string.printable:
    for j in string.printable:
        for k in string.printable:
            for l in string.printable:
                trysnum = trysnum + 1
                teststring = f'{i}{j}{k}{l}LiHua'
                m = hashlib.md5()
                m.update(teststring.encode())
                if trysnum <5:
                    print(m.hexdigest())
                if m.hexdigest().find(md5target)>=0:
                    print(teststring)
                    exit()
```

### MISCall

恢复git文件后执行恢复的脚本.但是有个坑点.win和linux的换行符不同,会导致结果不同.

### flag_universe

提取文件中再某个png图片中zsteg得到答案.

### Get-the-key.txt

要会挂载文件才行.注意,在wsl中,不能挂载在win的盘中,只能挂载在wsl的内部盘中.比如/tmp或者/mnt

挂完再复制出来即可.

```
mkdir /tmp/fore
sudo mount -o loop ./forensic100 /tmp/fore
sudo cp -r /tmp/fore/ .
sudo umount /tmp/fore
$  sudo grep -r key.txt
grep: 1: binary file matches
```

解压1得到结果.

### Reverse-it

需要知道常用文件头尾.

JPG是以FFD8开头,FFD9结尾.

题目名为反转,先从头到尾按字节反转,再每个字节内部半字节反转.可以用010editor的StringReverse加上NibblesReverse来解决.

### 打野

用zsteg -a即可看到答案.注意用zsteg还可以发现有wbstego隐写,用工具解压出来是乱码,是个误导项.

```
$ zsteg -a 瞅啥.bmp
[?] 2 bytes of extra data after image end (IEND), offset = 0x269b0e
extradata:0         .. ["\x00" repeated 2 times]
imagedata           .. text: ["\r" repeated 18 times]
b1,lsb,bY           .. <wbStego size=120, ext="\x00\x8E\xEE", data="\x1Ef\xDE\x9E\xF6\xAE\xFA\xCE\x86\x9E"..., even=false>
b1,msb,bY           .. text: "qwxf{you_say_chick_beautiful?}"
```

### 3-11

zsteg -a 发现有个zip包,解出来.

```
zsteg d0430db27b8c4d3694292d9ac5a55634.png -E b1,rgb,lsb,xy >1.zip
```

注意win自带的无法打开,用7zip才能打开.得到flag.txt,然后base64解码得到PNG文件.


### Become_a_Rockstar

```
(3.8.6/envs/env-3.8.6-py) nicroot@kaliwin:/mnt/f/trains/xctf/misc$ rockstar-py -i Become_a_Rockstar.rock -o become.py
(3.8.6/envs/env-3.8.6-py) nicroot@kaliwin:/mnt/f/trains/xctf/misc$ cat become.py
Leonard_Adleman = "star"
Problem_Makers = 76
Problem_Makers = "NCTF{"
def God(World):
    a_boy = "flag"
    the_boy = 3
def Evil(your_mind):
    a_girl = "no flag"
    the_girl = 5
...
...
(3.8.6/envs/env-3.8.6-py) nicroot@kaliwin:/mnt/f/trains/xctf/misc$ python3 become.py
6
8
NCTF{youar
nicerockstar
}
```

### 小小的PDF 

foremost直接得到隐藏图片.

### Cephalopod

查看流量包中有ceph协议,不用解密,wireshark中在最大的一个ceph流量包中能看到png文件头,导出分组字节流为png文件.

wp中则使用```tcpxtract -f  434c8c0ba659476caa9635b97f95600c.pcap```直接得到文件.

HITB{95700d8aefdc1648b90a92f3a8460a2c}

### labour

是个GPX地图数据

https://www.gpsvisualizer.com/map?output_home

把地图上传,每个点所在国家的首字母结合起来.

### hong

直接用foremost得到flag图片,二维码似乎没意义.这题binwalk拿不出图片.

BCTF{cute&fat_cats_does_not_like_drinking}

### misc_pic_again

zsteg发现有个zip包.提取出来,解压后发现有个可执行文件,strings它得到答案.

```
2000  zsteg -a 719af25af2ca4707972c6ae57060238e.png
 2001  zsteg  719af25af2ca4707972c6ae57060238e.png -E b1,rgb,lsb,xy >> haha.zip
 2002  file 1
 2003  strings 1
```

```
b8,rgb,lsb,Yx,prime .. text: "!C($8,\"1, 1)"
b8,bgr,lsb,Yx,prime .. text: "(C!,8$,1\")1 \","
nicroot@kaliwin:/mnt/f/trains/xctf/misc$ zsteg  719af25af2ca4707972c6ae57060238e.png -E b1,rgb,lsb,xy >> haha.zip
nicroot@kaliwin:/mnt/f/trains/xctf/misc$ file 1
1: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, too large section header offset 74309393851613184
nicroot@kaliwin:/mnt/f/trains/xctf/misc$ strings 1
/lib64/ld-linux-x86-64.so.2
libc.so.6
printf
__libc_start_main
__gmon_start__
GLIBC_2.2.5
UH-@
UH-@
[]A\A]A^A_
hctf{scxdc3tok3yb0ard4g41n~~~}
;*3$"
```

### low

画图打开另存为png,然后用stegoslove看到二维码
注意其它方式另存为png好像不行...bmp直接用stegoslove也不行.

flag{139711e8e9ed545e}

### 适合作为桌面

用stegoslove看到二维码,扫码得到hex,fromhex得到pyc文件. uncompyle6得到python代码.再得到flag串.

### 心仪的公司

strings流量包最后.

### misc1

在010editor中使用XOR 0X80,即每个字节第一位取0.

可能是通过观察这部分所有字节都大于128.转hex没成功.所以猜测第一位去掉,也就是减去128.

DDCTF{9af3c9d377b61d269b11337f330c935f}

### Miscellaneous-300

发现文件名就是解压密码,但是是一层套一层的.需要写脚本解压.

```python
import zipfile
import string
import os

num = 0
basepath = './'
openstring = '56197'

while num < 1000:
    floorszip =  zipfile.ZipFile("{}/{}.zip".format(basepath,openstring))
    if len(floorszip.filelist)==1:
        nextopenstring = floorszip.filelist[0].filename.split('.')[0]
        floorszip.extractall(path="./",pwd=nextopenstring.encode("ascii"))
        num = num + 1
        openstring = nextopenstring
        if openstring == '73168':
            exit()
    else:
        print(floorszip)
```