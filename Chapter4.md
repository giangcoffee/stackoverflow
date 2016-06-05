## Routing 
`Routing` hiểu đơn giản là cách ta tạo ra một đường link cho một trang trong ứng dụng web. Mỗi một trang cần một 
đường link duy nhất và giờ đây thì đường link đó còn cần phải đẹp, hay còn gọi là `friendly URL`. Một link đẹp là khi nhìn vào đường link đó 
ta có thể đoán được một cách đại khái nội dung mà trang sẽ hiển thị. Vì thế  hãy quên các đường link kiểu như `index.php?article_id=3`, link này 
không mang đủ thông tin cho người dùng.

Trong một dự án Symfony, tất cả `routing` đều được cấu hình tại một file duy nhất : `app/config/routing.yml` . Tuy nhiên, cơ chế  `import` 
cho phép các file cấu hình routing có thể nằm rải rác trong các bundle với điều kiện các file cấu hình cấp con phải được import ở trong 
file cấu hình cấp cha.

```
app:
    resource: "@AppBundle/Controller/"
    type:     annotation
```

Bên trên là file cấu hình mẫu khi lần đầu tiên bạn khởi tạo một project Symfony. `app` là tên mà bạn đặt cho đoạn cấu hình này.
Tên này là duy nhất trong một file cấu hình. `type` là tham số chỉ ra cách mà các routing được tạo ra. Ở đây nó mang giá trị `annotation` 
nghĩa là mỗi một đường link sẽ được gán trực tiếp ngay trên hàm thực thi của nó. Ví dụ :

```
/**
 * @Route("/", name="homepage")
 */
public function indexAction(Request $request)
{
  // replace this example code with whatever you need
  return $this->render('default/index.html.twig', [
    'base_dir' => realpath($this->getParameter('kernel.root_dir').'/..'),
  ]);
}
```

Thành phần đầu tiên `/` sẽ là đường link của trang, `homepage` là tên mà đặt con link này, nó dùng để trỏ đến trang mà không cần biết 
link thật sự là gì. Các bạn sẽ được học về cách dùng này trong cái bài sau.

Thành phần thứ 3 trong một đoạn cấu hình `routing` là `resource`, tham số này chỉ ra nơi sinh ra các routing. Như ví dụ ở trên thì `@AppBundle` 
là đường dẫn tương đối đến bundle `AppBundle` như vậy `@AppBundle/Controller/` nghĩa là tất cả các file trong thư mục `src/AppBundle/Controller/`
