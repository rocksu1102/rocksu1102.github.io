---
title: "Lần đầu làm chuyện ấy với Github"
excerpt_separator: "<!--more-->"
categories:
  - Github
tags:
  - Github
  
---

Công nhận "lần đầu làm chuyện ấy" với Github có nhiều điều bỡ ngỡ thật. Sau khi đã quen rồi thì mọi thứ sẽ dễ dàng hơn rất nhiều.

Trước tiên, cần chuẩn bị các thứ sau:

- Tài khoản github, nếu chưa có thì tạo mới.
- Tải và cài đặt git (git hỗ trợ tất cả OS luôn)

Khi mọi thứ đã xong, OK, Let's rock and roll nào:

Cấu hình git với username và email:

- Vào terminal và gõ các câu lệnh như bên dưới:

```yaml
$ git config --global user.name "Your name here"
$ git config --global user.email "your_email@example.com"
```

- Bước kế tiếp thích thì làm, không thích thì thôi:

```yaml
$ git config --global color.ui true
$ git config --global core.editor emacs
```
Chú thích:

Dòng đầu tiên là bật coloerd output trong terminal; dòng thứ hai là cho biết git sẽ dùng trình soạn thảo nào (mình dùng MacOS nên mình chọn emacs)

Cấu hình SSH:

- Kiểm tra xem bạn đã có các files này chưa 

```yaml
~/.ssh/id_rsa and ~/.ssh/id_rsa.pub
```

Đây là ssh private và public key

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

Hi username! You've successfully authenticated, but Github does
not provide shell access.
```

Nếu kết quả như bên trên thì chúc mừng, bạn đã thành công !!!

Túm lại, các bước mình cần làm là:
1. Cấu hình git với username và email (không bắt buộc)
2. Cấu hình SSH (bắt buộc)
