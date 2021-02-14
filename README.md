# update the kernel parameter to enable unattened installtion via iso file

/isolinux/isolinux.cfg
default install
label install
  menu label ^Install K8s Server
  kernel /install/vmlinuz
  append  preseed/file=/cdrom/preseed/k8s.seed auto=true debian-installer/locale=en_US console-setup/layoutcode=us ramdisk_size=16384 root=/dev/ram rw initrd=/install/initrd.gz quiet ---

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

mkdir ~/i
zcat boot/initrd.gz >~/i.cpio
cd ~/initrd
cpio -idv < ../i.cpio

find . | cpio --quiet -c -o | gzip -9 -n > /boot/initrd.gz

find . -type f -print0 | xargs -0 md5sum > md5sum.txt


rpm -ivh https://harbottle.gitlab.io/harbottle-main/7/x86_64/harbottle-main-release.rpm
yum install apt

# package file
apt-ftparchive generate config-deb
#release file

apt-ftparchive release k8s/dists/k8s > k8s/dists/k8s/Release

install dpkg on centos
yum install debootstrap.noarch

# ls /usr/share/debootstrap/scripts/
breezy  etch-m68k  hoary         jessie  maverick   potato   sarge             sid      testing   vivid         woody
dapper  feisty     hoary.buildd  karmic  natty      precise  sarge.buildd      squeeze  trusty    warty         woody.buildd
edgy    gutsy      intrepid      lenny   oldstable  quantal  sarge.fakechroot  stable   unstable  warty.buildd
etch    hardy      jaunty        lucid   oneiric    raring   saucy             stretch  utopic    wheezy

