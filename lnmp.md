- libxml2 `ftp://xmlsoft.org/libxml2/`

- libmcrypt `ftp://mcrypt.hellug.gr/pub/crypto/mcrypt/libmcrypt/libmcrypt-2.5.7.tar.gz`

- mhash `http://jaist.dl.sourceforge.net/project/mhash/mhash/0.9.9.9/mhash-0.9.9.9.tar.gz`

- mcrypt `http://jaist.dl.sourceforge.net/project/mcrypt/MCrypt/2.6.8/mcrypt-2.6.8.tar.gz`

- zlib `http://zlib.net/`

- libpng `ftp://ftp.simplesystems.org/pub/libpng/png/src/libpng16/libpng-1.6.24.tar.gz`

- jpeg9 `http://www.ijg.org/files/jpegsrc.v9b.tar.gz`

- freetype `http://download.savannah.gnu.org/releases/freetype/freetype-2.6.tar.gz`

- gd `https://github.com/libgd/libgd/releases/download/gd-2.2.3/libgd-2.2.3.tar.gz`



> 多命令顺序执行：
>
>	&&		命令1正确执行，命令2才会执行
>
>	||		命令1不正确执行，命令2才会执行
>
>	；	   命令1执行完成，命令2执行
>
>	|       命令1的执行结果，作为命令2 的操作对象

### 安装libxml2

> libxml是一个用来解析XML文档的函数库。它用C语言写成, 并且能为多种语言所调用，例如C语言，C++，XSH。C#, Python，Kylix/Delphi，Ruby，和PHP等。Perl中也可以使用XML::LibXML模块。它最初是为GNOME开发的项目，但现在可以用在各种各样的方面。libXML 代码可移植性非常好，因为它基于标准的ANSI C库, 并采用MIT许可证。

#### centos:

`yum -y install python-devel`  
*`yum  install  -y  libxml2-devel`	如果报错，安装此包后再尝试安装*


#### debian/ubuntu:

`apt-gei install -y python-dev`  
*`apt-get install  -y  libxml2-dev`	如果报错，安装此包后再尝试安装*

    cd libxml2-2.9.4
    ./configure --prefix=/usr/local/libxml2
    make && make install

### 安装libmcrypt

> libmcrypt是加密算法扩展库。支持DES, 3DES, RIJNDAEL, Twofish, IDEA, GOST, CAST-256, ARCFOUR, SERPEN T, SAFER+等算法。


#### centos:

`centos: yum -y  install  gcc-c++`


#### debian/ubuntu:

`debian/ubuntu: apt-get install -y g++`

    cd libmcrypt-2.5.7
    ./configure --prefix=/usr/local/libmcrypt/
    make && make install

*需调用gcc-c++编译器，未安装会报错*


### 安装libltdl，也在libmcrypt源码目录中，非新软件

    cd libltdl
    ./configure --enable-ltdl-install
    make && make install


### 安装mhash

> Mhash是基于离散数学原理的不可逆向的php加密方式扩展库，其在默认情况下不开启。mhash的可以用于创建校验数值，消息摘要，消息认证码，以及无需原文的关键信息保存（如密码）等。

    cd mhash-0.9.9.9
    ./configure
    make && make install


### 安装mcrypt

> mcrypt 是 php 里面重要的加密支持扩展库。Mcrypt库支持20多种加密算法和8种加密模式。

    cd mcrypt-2.6.8
    LD_LIBRARY_PATH=/usr/local/libmcrypt/lib:/usr/local/lib ./configure --with-libmcrypt-prefix=/usr/local/libmcrypt

    # 以上为一条命令。LD_LIBRARY_PATH用于指定libmcrypt和mhash的库的位置。  
    --with-libmcrypt-prefix用于指定libmcrypt软件位置。

    make && make install

*mcrypt没有安装完成，这是php的模块，需要等php安装完成之后，再继续安装*


### 安装zlib

> zlib是提供数据压缩用的函式库，由Jean-loup Gailly与Mark Adler所开发，初版0.9版在1995年5月1日发表。zlib使用DEFLATE算法，最初是为libpng函式库所写的，后来普遍为许多软件所使用。此函式库为自由软件，使用zlib授权。

    cd zlib-1.2.8
    ./configure
    make
    make install >> /root/zlib.log

*zlib指定安装目录可能造成libpng安装失败，故不指定，为卸载方便，建议make install执行结果输出到安装日志文件，便于日后卸载*


### 安装libpng

> libpng 软件包包含 libpng 库.这些库被其他程式用于解码png图片

    cd libpng-1.6.24
    ./configure --prefix=/usr/local/libpng
    make && make install


### 安装jpeg6

> 用于解码.jpg和.jpeg图片

    mkdir -p /usr/local/jpeg6/{bin,lib,include,man/man1}

    # 目录必须手工建立

    cd jpeg-9b
    ./configure --prefix=/usr/local/jpeg9/ --enable-shared --enable-static
    make && make install
*--enable-shared与--enable-static参数分别为建立共享库和静态库使用的libtool*


### 安装freetype

> FreeType库是一个完全免费(开源)的、高质量的且可移植的字体引擎，它提供统一的接口来访问多种字体格式文件，包括TrueType, OpenType, Type1, CID, CFF, Windows FON/FNT, X11 PCF等。支持单色位图、反走样位图的渲染。FreeType库是高度模块化的程序库，虽然它是使用ANSI C开发，但是采用面向对象的思想，因此，FreeType的用户可以灵活地对它进行裁剪。

    cd freetype-2.6
    ./configure --prefix=/usr/local/freetype/
    make && make install


### 安装GD库

> GD库，是php处理图形的扩展库，GD库提供了一系列用来处理图片的API，使用GD库可以处理图片，或者生成图片。 在网站上GD库通常用来生成缩略图，或者用来对图片加水印，或者用来生成汉字验证码，或者对网站数据生成报表等。

    cd libgd-2.2.3

    # png错误，修改方法：
    # vi rc/gd_png.c
    # 把 #include “png.h” 替换为 #include "/usr/local/libpng/include/png.h"

    ./configure --prefix=/usr/local/gd2/ --with-jpeg=/usr/local/jpeg6/ --with-freetype=/usr/local/freetype/ --with-png=/usr/local/libpng/
    make CFLAGS="-Wno-error"
    make install
*若前面配置zlib时没有指定安装目录，gd配置时不要添加--with-zlib=/usr/local/zlib/参数*


### 安装php

    apt-get install libtool*
    apt-get install libxpm-dev
    
    ln -s /usr/lib/x86_64-linux-gnu/libXpm.so /usr/lib/
    ln -s /usr/lib/x86_64-linux-gnu/libXpm.a /usr/lib/

    cd php-7.0.10
    ./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --with-libxml-dir=/usr/local/libxml2/ --with-jpeg-dir=/usr/local/jpeg9/ --with-png-dir=/usr/local/libpng/ --with-freetype-dir=/usr/local/freetype/ --with-gd=/usr/local/gd2/ --with-mcrypt=/usr/local/libmcrypt/ --enable-soap --enable-mbstring=all --enable-sockets --without-pear --with-xpm-dir=/usr/lib64/ --enable-fpm
    make && make install





