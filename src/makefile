#download latest GCC in https://github.com/miao1007/Openwrt-NetKeeper/wiki#2-%E5%A6%82%E4%BD%95%E4%B8%8B%E8%BD%BDgcc
#This is a demo for MTK7620A

#TODO:填写解压的Toolchain中bin与include所在的目录（根目录）,某些奇葩可能用的是glibc，这里可能要替换LIBC
LOCATION=../../OpenWrt-Toolchain-ramips-for-mipsel_24kec+dsp-gcc-4.8-linaro_uClibc-0.9.33.2/toolchain-mipsel_24kec+dsp_gcc-4.8-linaro_uClibc-0.9.33.2
#TODO:请注意不同型号(mips/mipsel)路由器此处gcc文件名可能略有不同
CC=$(LOCATION)/bin/mipsel-openwrt-linux-gcc
#TODO:可能需要修改pppd的版本，取决于路由器的/usr/lib/pppd/，目前主流的14.09是2.4.7
PPPD_VER=2.4.7
CFLAGS=-Os -Werror -I$(LOCATION)/include -fPIC -DPPPOE_VER='"${PPPD_VER}"'

# TODO: change RADIUS
# 
# ChongQing Netkeeper: cqxinliradius002
# ChongQing Netkeeper(0094): xianxinli1radius
# WuHan E xin: hubtxinli01
# Hangzhou(Tested on HDU): singlenet01
# qinghai 3.6.27: shd@xiaoyuan0002
# Xinjiang 3.7.3 : xinjiang@0724
# hebei: hebeicncxinli002
# ShanDong Mobile : shandongmobile13
# Shanxi Yixun : sh_xi@xiaoyuan01
# GanSu Telecom 3.7.1 : xiaoyuanyixun001

##  The following radius has been deprecated due to update. No more used.
#
# ShanDong Telecom : 560Ox!a0yuanOlIz  (For 3.7.3 Augest Version)
# ShanDong Telecom : shdOx!a0yuan01lz  (For 3.7.3 October 27th Version)
# NanChangV12~V17: radius
# NanChangV18~V29: nanchang3.0
# NanChangV32: jiangxi4.0
#

# TODO: Change PREFIX1
# 
# NanChangV32: '1'
# Others: '\n'

all:chongqing_sxplugin chongqing0094_sxplugin hubei_sxplugin zhejiang_xiaoyuan_sxplugin xinjiang_sxplugin qinghai_sxplugin shandongmobile_sxplugin hebei_sxplugin shanxi_yixun_sxplugin gansu_telecom_sxplugin zhejiang_qiye_sxplugin hainan_sxplugin
	@find *.so
	@echo "拨号组件编译成功，注意修改confnetwork.sh的sxplugin名称为本省的名称，以及拨号帐号与密码!，然后运行make upload"

#you can also upload only your province's so file
upload:
	@echo "正在上传拨号组件，请输入路由器ssh密码"
	scp *.so root@192.168.1.1:/usr/lib/pppd/${PPPD_VER}/
	@echo "正在上传网络配置脚本，请输入路由器ssh密码"
	scp confnetwork.sh root@192.168.1.1:/tmp/
	@echo "正在登录路由器，请在输入路由器ssh密码后，运行sh /tmp/confnetwork.sh"
	ssh root@192.168.1.1

chongqing0094_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"xianxinli1radius"'  -DPREFIX1="'\n'" -shared -o $@.so
	
chongqing_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"cqxinliradius002"'  -DPREFIX1="'\n'" -shared -o $@.so

hubei_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"hubtxinli01"' -DPREFIX1="'\n'" -shared -o $@.so

zhejiang_xiaoyuan_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"singlenet01"' -DPREFIX1="'\n'" -shared -o $@.so

xinjiang_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"xinjiang@0724"' -DPREFIX1="'\n'" -shared -o $@.so
	
qinghai_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"shd@xiaoyuan0002"'  -DPREFIX1="'\n'" -shared -o $@.so

shandongmobile_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"shandongmobile13"' -DPREFIX1="'\n'" -shared -o $@.so

hebei_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"hebeicncxinli002"' -DPREFIX1="'\n'" -shared -o $@.so
	
shanxi_yixun_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"sh_xi@xiaoyuan01"' -DPREFIX1="'\n'" -shared -o $@.so

gansu_telecom_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"xiaoyuanyixun001"' -DPREFIX1="'\n'" -shared -o $@.so
	

ningxia_telecom_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"n_x@xiaoyuanwang"' -DPREFIX1="'\n'" -shared -o $@.so

zhejiang_qiye_sxplugin:
	@$(CC) $(CFLAGS) sxplugin.c -DRADIUS='"zjxinlisx02"' -DPREFIX1="'\n'" -shared -o $@.so

hainan_sxplugin:
	@$(CC) $(CFLAGS) hainan_sxplugin.c -shared -o $@.so

#clean *.so 
clean:
	rm *.so
