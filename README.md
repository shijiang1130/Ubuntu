https://git.kernel.org/pub/scm/boot/syslinux/syslinux.git/    ？=  https://github.com/geneC/syslinux

https://releases.ubuntu.com/16.04/

https://help.ubuntu.com/community/LiveCDCustomizationFromScratch
https://help.ubuntu.com/lts/installation-guide/amd64/apb.html
isolinux.cfg 是 ISO、光盘 引导的主入口。
menu.cfg 在 syslinux.cfg 被 include ，按需修改。
splash.png 是启动画面，按需修改。
txt.cfg 在 menu.cfg 被 include ，添加 auto 和 file 参数。

copy kfile 
d-i  preseed/late_command       string cp -frv /cdrom/extra/* /opt/

or run script
d-i preseed/late_command string in-target wget --output-document=/tmp/post-install.sh http://192.168.？.？/post-install.sh; in-target /bin/sh /tmp/post-install.sh

mkisofs  -o  k8s.iso   -b  isolinux/isolinux.bin  -c  isolinux/boot.cat  -no-emul-boot -boot-load-size 4 -boot-info-table -R -J -v -T ./

cd /media/cdrom/pool/extras
apt install ebtables
dpkg -i cri-tools*.deb
dpkg -i lib*.deb
dpkg -i socat*.deb
dpkg -i con*.deb
dpkg -i docker*.deb
dpkg -i kube*.deb
dpkg -i linux-*.deb


unsquashfs filesystem.squashfs
mksquashfs dir/ filesystem.squashfs1
du -sx --block-size=1 ./ | cut -f1 > dir/install/filesystem.size



https://help.ubuntu.com/community/InstallCDCustomization#Modify_pool_structure_to_include_more_packages


install dpkg on centos
yum install debootstrap.noarch

# ls /usr/share/debootstrap/scripts/
breezy  etch-m68k  hoary         jessie  maverick   potato   sarge             sid      testing   vivid         woody
dapper  feisty     hoary.buildd  karmic  natty      precise  sarge.buildd      squeeze  trusty    warty         woody.buildd
edgy    gutsy      intrepid      lenny   oldstable  quantal  sarge.fakechroot  stable   unstable  warty.buildd
etch    hardy      jaunty        lucid   oneiric    raring   saucy             stretch  utopic    wheezy

https://wiki.syslinux.org/wiki/index.php?title=ISOLINUX
