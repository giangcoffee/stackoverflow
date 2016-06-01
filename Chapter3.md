## Bundle trong Symfony 

Như đã nói ở chương trước `bundle` được coi là thành phần cơ bản của Symfony, mỗi một project Symfony đều được cấu thành từ 
nhiều bundles riêng lẻ, bao gồm cả các thư viện nằm trong thư mục `vendor`. Các bundle đều có cấu trúc chung nhất gồm các thành phần không thể thiếu như : Một class extends `Symfony\Component\HttpKernel\Bundle\Bundle` class này được dùng để kích hoạt bundle trong `AppKernel`, `DependencyInjection` dùng để khai báo các thư viện mà bundle cần để hoạt động . Ngoài ra thì bundle có thể các thư mục phổ biến khác như `Controller`, `Resources`, `Tests` hay bất cú thư mục nào mà lập trình viên thấy cần. 

Bundle có thể được tạo thủ công bằng cách tập hợp mã nguồn theo thư mục như nói ở trên nhưng Symfony cũng có các công cụ có sẵn để giúp bạn có thể có được một cấu trúc chung nhất cho bundle của mình. Đây là lúc chúng ta dùng đến tool `app/console` như đã nói ở chương trước.

```
$ cd [project name]
$ php app/console 
```

Các dòng màu xanh là các công cụ có sẵn giúp chúng ta dễ dàng thao tác với một project Symfony, đầu tiên là công cụ tạo bundle tự động :

```
$ php app/console generate:bundle [tên bundle gồm cả namesspace]
```

Tên một bundle thường gồm hai phần, thứ nhất là vendor - đơn giản là tên công ty sở hữu project này, thứ hai là tên bundle , mô tả một cách đầy đủ và ngắn gọn về tác dụng của bundle , quan trọng là nó phải kết thúc bằng cụm từ `Bundle`. Ví dụ bạn có thể gõ :

```
$ php app/console generate:bundle Google/DownloadChromeBundle
```

Enter khi được hỏi về default targer directory, chọn `yml` cho `configuration format` (cái này là theo kinh nghiệm cá nhân) còn những cái khác các bạn có thể chọn mặc định (Enter không phải nghĩ +1 )

Một cấu trúc thư mục sẽ được tạo ra trong `src` tùy vào namespace mà bạn cung cấp. Như ví dụ ở trên thì thư mục `Google` sẽ được tạo ra và một file `GoogleDownloadChromeBundle.php` trong thư mục đó. Thứ hai là namespace bạn cung cấp sẽ được thêm vào trong `AppKernel` để kích hoạt bundle. Cuối cùng là một dòng cấu hình sẽ được thêm vào `app/config/routing.yml` trong đó trỏ đến `Controller/DefaultController.php` nằm trong bundle mới tạo ra của bạn.

Vì ngoài các bundles ra còn có thể vô số các thư mục khác có thể được thêm vào trong thư mục gốc `src` nên để cho dễ dàng bạn có thể cho tất các các bundle vào chung một thư mục bằng cách thay đổi `namespace` khi tạo bundle :

```
$ php app/console generate:bundle Google/Bundles/DownloadChromeBundle
```

Như vậy tất cả các bundle của bạn sẽ được lưu vào chung thư mục `src/Google/Bundles`.
