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

Thư mục này chỉ chứa một vài file và thư mục nhưng nó điều khiên hoạt động của cá project. Hầu như tất cả mã nguồn của project đều nằm ở thư mục khác, gọi là các `bundles` nhưng chúng được kích hoạt trong class `AppKernel`, được cấu hình ở file `config/config.yml` cũng nằm trong thư mục `app` này. Mỗi `bundle` là tập hợp một vài file mã nguồn làm một công việc nào đó, `bundle` có thể ở dạng chia sẻ giữa các project hoặc có thể chỉ tồn tại ở một project duy nhất. Để tạo ra một `bundle` chia sẻ giữa các project cần một số cấu hình đặc biệt mà chúng ta sẽ bàn đến trong một khóa học khác. 

Tất cả URL trong trang web của bạn sẽ được điều khiển trong file `routing.yml`, là cách mà người dùng sẽ gõ trên browser để đến được với những nội dung trên web. 

Một số file quan trọng khác như `app/console` hay `app/Resources/views/base.html.twig` thì chúng ta sẽ nói rõ hơn trong quá trình học.

**src**

Đây là nơi chứa phần lớn mã nguồn của project, được chia ra thành các `bundle`, mỗi `bundle` thực hiện một nhiệm vụ và thường nằm trong một thư mục riêng với hậu tố `Bundle`. Ví dụ như ở project demo sẽ có thư mục `AcmeDemoBundle` trong thư mục `src`.

**vendor** 

Như đã trình bày ở phần `Composer` thì đây là nơi chứa mã nguồn các thư viện sử dụng trong project, trong hầu hết trường hợp thì bạn không cần quan tâm trong này có gì, trừ khi bạn muốn tìm hiểu sâu về một bundle nào đó.

**web** 

Đây chính là thư mục gốc (document root) trên web server hay web hosting trong trường hợp bạn không dùng web server có sẵn của Symfony, vì thế tất cả file trong thư mục này sẽ được truy cập public. Những file thường được đặt trong thư mục này gồm : javascript, CSS, ảnh và font files. Có hai file thực sự tiếp nhận các request từ phía user đó là `app_dev.php` - nếu môi trường là `dev` (chạy trên máy của bạn) và `app.php` - nếu môi trường là `production` (chạy thật trên web hosting). Hai file này giống như hai cánh cửa duy nhất dẫn đến trang web của bạn, bạn có thể cài đặt bảo vệ ở hai cánh cửa này theo cách bạn muốn (firewalls, ACL ...) trong file `app/config/security.yml`.
