# ubuntu

rrdtool 1.5 for ubuntu 16.10 build

wget https://oss.oetiker.ch/rrdtool/pub/rrdtool-1.5.6.tar.gz
apt-get install libpango1.0-dev libxml2-dev

unknown group 'smmsp' in statoverride file

~# cat /var/lib/dpkg/statoverride
geoclue geoclue 755 /var/lib/geoclue
root smmsp 2755 /usr/lib/sm.bin/sendmail
root lp 775 /var/log/hp/tmp
root postdrop 2555 /usr/sbin/postqueue
postfix postdrop 2710 /var/spool/postfix/public
root crontab 2755 /usr/bin/crontab
root Debian-exim 640 /etc/exim4/passwd.client
root mlocate 2755 /usr/bin/mlocate
root root 1733 /var/lib/php/sessions
root ssl-cert 710 /etc/ssl/private
hplip root 755 /var/run/hplip
root smmsp 2755 /usr/lib/sm.bin/mailstats
root messagebus 4754 /usr/lib/dbus-1.0/dbus-daemon-launch-helper
root postdrop 2555 /usr/sbin/postdrop

~# dpkg-statoverride --remove /usr/lib/sm.bin/sendmail
~# dpkg-statoverride --remove /usr/lib/sm.bin/mailstats
~# cat /var/lib/dpkg/statoverride                      
geoclue geoclue 755 /var/lib/geoclue
root smmsp 2755 /usr/lib/sm.bin/sendmail
root lp 775 /var/log/hp/tmp
root postdrop 2555 /usr/sbin/postqueue
postfix postdrop 2710 /var/spool/postfix/public
root crontab 2755 /usr/bin/crontab
root Debian-exim 640 /etc/exim4/passwd.client
root mlocate 2755 /usr/bin/mlocate
root root 1733 /var/lib/php/sessions
root ssl-cert 710 /etc/ssl/private
hplip root 755 /var/run/hplip
root messagebus 4754 /usr/lib/dbus-1.0/dbus-daemon-launch-helper
root postdrop 2555 /usr/sbin/postdrop

BUILD_DIR=/tmp/rrdbuild
INSTALL_DIR=/opt/rrdtool

 mkdir -p $BUILD_DIR
 cd $BUILD_DIR
 
 gunzip -c rrdtool-1.5.6.tar.gz | tar xf -
 cd rrdtool-1.5.6
 ./configure --prefix=$INSTALL_DIR && make && make install
 
