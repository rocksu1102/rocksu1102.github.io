---
title: "Lần đầu làm chuyện ấy với Github"
excerpt_separator: "<!--more-->"
categories:
  - Github
tags:
  - Github
  
---

Công nhận "lần đầu làm chuyện ấy" với Github có nhiều điều bỡ ngỡ thật. Sau khi đã quen rồi thì mọi thứ dễ dàng hơn rất nhiều

Trước tiên, bạn cần chuẩn bị:

- Tài khoản github
- Tải và cài đặt git.
- Cấu hình git với username và email

OK, sau khi mọi thứ đã xong, bạn mở terminal/shell:

```yaml
$ git config --global user.name "Your name here"
$ git config --global user.email "your_email@example.com"
```

Như vậy là xong phần cấu hình git với username và email, với mình thì cấu hình thêm các option sau:

```yaml
$ git config --global color.ui true
$ git config --global core.editor emacs
```
Dòng đầu tiên là bật coloerd output trong terminal; dòng thứ hai là cho biết git sẽ dùng trình soạn thảo nào (mình dùng MacOS nên mình chọn emacs)

- Bước tiếp theo là mình cấu hình SSH trên máy mình đang dùng, các bước làm như sau:
    - Kiểm tra xem bạn đã có các files này chưa ~/.ssh/id_rsa and ~/.ssh/id_rsa.pub (đây là ssh private và public key)
    - Nếu chưa thì tiến hành tạo, mở terminal và gõ:

```yaml
$ ssh-keygen -t rsa -C "your_email@example.com"
```

    - Copy ssh public key (nội dung bên trong của file id_rsa.pub)
    - Sau đó, paste nội dung này vào tài khoản github của mình bằng cách:
      - Đăng nhập vào github và vào Account Settings
      - Click "SSH Keys" 
      - Click "Add SSH Key" 
      - Đặt tên label (My SSH Key), sau đó paste nội dung public key vào khung text box.
      - Sau đó, quay lại màn hình terminal để kiểm tra kết quả

```yaml
$ ssh -T git@github.com
```

      - Nếu kết quả như bên dưới thì chúc mừng, bạn đã thành công !!!

```yaml
Hi username! You've successfully authenticated, but Github does
not provide shell access.
```

URL: https://kbroman.org/github_tutorial/pages/first_time.html
