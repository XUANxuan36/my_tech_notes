dddvdvb文件类别识别

1. **File命令**

当文件后缀名无法准确显示而使文件无法打开时，在linux使用file+文件名可以识别出文件的后缀，修改正确后可打开

2. **查看文件头**

使用010可查看文件头类型，文件的16进制内容，头尾可能隐含flag

![](图片\misc\1744471487426-1ddee1f5-2513-4bc6-a9f5-861e971aea60.png)

3. **使用stegsolve**

File Format:文件格式

Data Extract:数据提取

Steregram Solve:立体试图 左右控制偏移

Frame Browser:帧浏览器

Image Combiner:拼图 图片拼接

4. **分离图片**

**有时候图片会包含其他的文件**

![](图片\misc\1744471487620-d0428536-fa4a-4b58-9220-1225a12a9312.png)

先使用binwalk查看图片

binwalk -e pcat.bin //要分解的文件名

也可使用foremost分离文件，文件会放在output文件夹里

5. 图片内容不显示完全，高度或宽度被修改

使用以下工具

![](图片\misc\1744471487762-fe230ec0-bc15-4d7b-b341-bc6fbaf150be.png)

```plain
python3 -m pip install -r requirements.txt
python3 main.py -i dabai.png
```

![](图片\misc\1744471487920-237e1bb5-742d-48f7-956e-4fde43781d57.png)

去010修改文件高度和宽度



6. **恢复删除文件**

```plain
extundelete disk-image --restore-all
```

7. **查看图片隐写**

```plain
zsteg -a steg.png  
```

8. **盲水印**

```plain
python bwmforpy3.py decode day1.png day2.png flag.png –oldseed
python2 bwm.py decode day1.png day2.png flag.png
```



![](图片\misc\1744471488137-35028d01-2bfe-43a6-a9d8-a5ebc70aae49.png)

1. **摩斯密码只有01**
2. **分离gif图片**

![](图片\misc\1744471488401-e1aec9e7-8ab3-49dd-b85b-f2e342bb7d87.png)

**conver 分离文件路径 生成文件路径**

**montage //合并文件**

![](图片\misc\1744471488563-671e79f3-55ff-477b-bb29-bbb4dc825169.png)

**-tile是拼接时每行和每列的图片数，这里用x1，就是只一行**

**-geometry是首选每个图和边框尺寸，我们边框为0，图照原始尺寸即可**

1. **暴力破解压缩包**

**fcrackzip工具**

**	使用方法：fcrackzip -b -c -l -u**

![](图片\misc\1744471488758-2b76f29e-0f86-449c-9dfb-4fc6c6bb7f27.png)

**rarcrack这个工具**

**rarcrack 1.rar --threads 1000 --type rar**





1. **文件倒转**

cd FileReverse-Tools

python3 FileReverse-Tools.py -i /home/kali/Desktop/ping

![](图片\misc\1744471488963-b6a1b66b-fd8e-4ef5-81d8-66e56ed3f99a.png)



1. **Snow隐写**

![](图片\misc\1744471489154-72e2dcba-74cc-474d-b939-241c95ea5f96.png)

# 流量分析
<u>usb流量</u>：8字节为键盘输入，4字节为鼠标

**1、键盘流量**

USB协议数据部分在Leftover Capture Data域中，数据长度为八个字节。其中键盘击键信息集中在第三个字节中。

**2、鼠标流量**

USB协议鼠标数据部分，在Leftover Capture Data域中，数据长度为四个字节。

其中第一个字节代表按键，当取0x00时，代表没有按键、为0x01时，代表按左键，为0x02时，代表当前按键为右键。第二个字节可以看成是一个signed byte类型，其最高位为符号位，当这个值为正时，代表鼠标水平右移多少像素，为负时，代表水平左移多少像素。第三个字节与第二字节类似，代表垂直上下移动的偏移。



<u>Wav音频文件</u>：使用Audacity查看频谱图

