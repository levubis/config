Công Nghệ VPS - SuPHP + Apache
======

Congnghevps | Config SuPHP + Apache

TUT http://congnghevps.net/2013/11/cau-hinh-suphp-voi-centos-6.html

Add repo

[epel]  
 name=Extra Packages for Enterprise Linux 6 - $basearch  
 #baseurl=http://download.fedoraproject.org/pub/epel/6/$basearch  
 mirrorlist=https://mirrors.fedoraproject.org/metalink?repo=epel-6&arch=$basearch  
 failovermethod=priority  
 enabled=1  
 gpgcheck=0  
 gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6  
 [rpmforge]  
 name = RHEL $releasever - RPMforge.net - dag  
 baseurl = http://apt.sw.be/redhat/el6/en/$basearch/rpmforge  
 mirrorlist = http://apt.sw.be/redhat/el6/en/mirrors-rpmforge  
 #mirrorlist = file:///etc/yum.repos.d/mirrors-rpmforge  
 enabled = 1  
 protect = 0  
 gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmforge-dag  
 gpgcheck = 0  
 
yum install suphp -y

Tuy nhiên trước đó nếu các bạn chưa cài đặt php, apache và mysql thì các bạn cần chạy lệnh sau đây để cài đặt đầy đủ các thành phần.

yum install httpd mysql-server php-ZendFramework-full -y
Tiếp theo các bạn chỉnh sửa file /etc/httpd/conf.d/suphp.conf , xóa hết các dòng hiện có và chỉ để lại hai dòng sau đây

LoadModule suphp_module modules/mod_suphp.so  
suPHP_Engine off  

Sau đó các bạn tiếp tục chỉnh sửa file /etc/suphp.conf , thêm dấu ” và ” vào trong 2 dòng config cuối cùng sau dấu =, cụ thể là sau khi chỉnh sửa sẽ trông như thế này

 [handlers]  
 ;Handler for php-scripts  
 x-httpd-php="php:/usr/bin/php" // Có dấu " và " thêm vào  
 ;Handler for CGI-scripts  
 x-suphp-cgi="execute:!self" // Có dấu " và " thêm vào  
 
Virtualhost Demo 

<VirtualHost *:80>  
 ServerName [congnghevps.net]  
 ServerAdmin   [info@congnghevps.net]  
 DocumentRoot  [/home/congnghevps/www]  
 suPHP_Engine on  
 suPHP_UserGroup [congnghevps] [congnghevps]  
 AddHandler x-httpd-php .php .php3 .php4 .php5  
 suPHP_AddHandler x-httpd-php  
 </VirtualHost>  
