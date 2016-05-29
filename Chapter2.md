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

Cách khởi tạo một project Symfony bằng bộ Symfony Installer được trình bày trên trang chủ của Symfony project :

```
$ sudo curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony
$ sudo chmod a+x /usr/local/bin/symfony
```

Hai lệnh trên dùng để download bộ Symfony Installer thành một lệnh trên máy tính của bạn.

**Khởi tạo một project Symfony**

```
$ symfony new [tên project]
hoặc 
$ composer create-project symfony/framework-standard-edition [tên project] @stable
```
Hai lệnh trên sẽ mất một khoảng thời gian để chạy xong tùy thuộc vào tốc độ kết nối internet của bạn. Bộ composer sẽ đọc file `composer.json` của bạn để biết được project Symfony của bạn cần những thư viện nào. Sau khi tất cả mã nguồn của tất cả các thư viện phụ thuộc được download về một thư mục, gọi là `vendor` thì quá trình tự động cài đặt sẽ diễn ra. Bộ cài đặt sẽ hỏi các bạn về một số tham số nhưng để đơn giản các bạn có thể chập nhận các giá trị mặc định bằng cách Enter mỗi khi được hỏi. Ý nghĩa các tham số này sẽ được trình bày trong các chướng kế tiếp.

**Cấu hình web server**

`Web server` mà bạn dự định triển khai trên đó cần thỏa mãn một số yêu cầu. Symfony có một chức năng riêng dùng để tự động kiểm tra vấn đề này `web/config.php`. Tuy nhiên nếu trên máy của bạn đang chạy PHP phiên bản 5.4 trở lên thì bạn có thể sử dụng luôn bộ web server có sẵn của Symfony như sau :

```
$ cd [tên project]
$ cd web
$ php -S localhost:8000
```

một trang web sẽ được chạy trên máy tính của bạn lắng nghe ở cổng `8000` và bạn có thể kiểm tra luôn web server của bạn có tương thích không bằng cách mở trên browser [http://localhost:8000/config.php](http://localhost:8000/config.php). Để trang web có thể chạy bình thường thì bạn cần sửa các lỗi quan trọng (Major problems) hiển trị trên trang `config.php` còn các lỗi nhỏ (Minor problems) thì có thể bỏ qua. Vấn đề này sẽ được trình bày chi tiết hơn vào một khóa học khác.

**Các lỗi thường gặp khi khởi tạo**

Lỗi thường gặp nhất khi lần đầu chạy một project Symfony là lỗi về permission ở hai thư mục `app/cache/` và `app/logs`. Hai thư mục này dùng để lưu cache và logs của project cho nên cần quyền ghi và đọc cho user của web server, thường là `www-data`. Dĩ nhiên khi bạn dùng web server của Symfony thì user mà bạn log in cũng là user web server nên vấn đề  này sẽ không xảy ra.

Nếu bạn đang dùng `Apache2` và gặp phải vấn đề này thì cách đơn giản nhất để giải quyết là mở khóa dòng code `umask(0000)` trong file `web/app_dev.php` nếu bạn đang chạy trên môi trường`dev`. Dòng lệnh này đảm bảo các file trong thư mục cache và logs được tạo ra với mode 777 tức là được đọc ghi với tất cả các user. Việc còn lại là :

```
$ chmod -R 777 app/cache/* app/logs/*
```
 Đến đây các bạn sẽ không gặp lỗi nào về permission nữa nhưng nếu vẫn muốn tìm hiểu thêm các bạn có thể tham khảo [Link sau](http://symfony.com/doc/current/book/installation.html#book-installation-permissions).

## Cấu trúc thư mục 

**app**

Thư mục này chỉ chứa một vài file và thư mục nhưng nó điều khiên hoạt động của cá project. Hầu như tất cả mã nguồn của project đều nằm ở thư mục các, gọi là các `bundles` nhưng chúng được triệu gọi trong class `AppKernel`, được cấu hình ở file `config.yml` nằm trong thư mục `app` này.  
