## Tạo mới một project Symfony 

Hiện tại có hai cách chính để có thể khởi tạo một project `Symfony` đó là dùng hai tool `composer.phar` và `symfony.phar`.
Chi tiết các bạn có thể tham khảo ở [Link này](http://symfony.com/download). 

**Composer**

`Composer` là trình quản lý gói được sử dụng chính thức trong các project Symfony, tiện ích này có nhiệm vụ download, update các thư
viện sử dụng trong một project Symfony, đặt chúng vào những vị trí định sẵn, đồng thời quản lý bằng `namespace`. Để cài 
đặt Composer các bạn cần có `curl` và `PHP`. Nếu chưa cài đặt các bạn có thể dùng lệnh sau :

```
$ sudo apt-get install php5 
$ sudo apt-get install curl 
```

Để donwload bản composer mới nhất các bạn làm như sau :

```
$ curl -s https://getcomposer.org/installer | php
$ mv composer.phar /usr/local/bin/composer
$ sudo chmod a+x /usr/local/bin/composer 
```

Dòng lệnh thứ hai và ba dùng để cài đặt composer thành lệnh của hệ thống nghĩa là các bạn có thể gõ lệnh `composer` trên command
line giống như các lệnh khác như `cd` hay `ls`.

**Symfony installer**

Cách thứ 


