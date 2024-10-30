---
title: "Open Source SSG"
date: 2022-10-10
weight: 6
# aliases: ["/first"]
tags: [web, software]
author: Dung
summary: Cá nhân hóa website cùng Static Site Generator
showToc: true
TocOpen: true
description: Kiến trúc tiêu chuẩn ngành Automotive
hideSummary: false
ShowWordCount: false
ShowReadingTime: true
ShowPostNavLinks: false

editPost:
    Text: Xem tại VIBLO
    URL: https://viblo.asia/p/open-source-ssg-ca-nhan-hoa-website-cung-static-site-generator-7ymJXxkEJkq
    appendFilePath: false # to append file path to Edit link
---
\
![LeetCode Badges](https://leetcode-badge-showcase.vercel.app/api?username=du4ng)​

##  1. Giới thiệu

Một ngày đẹp trời, mình tình cờ vấp phải [**That IELTS Guide 🌱**](https://thatieltsguide.com/) của thầy Quang. Mình nghĩ, chắc cũng là một kiểu build blog cá nhân, như các bạn Content/Copywriter vẫn hay dùng, sử dụng các nền tảng như Wordpress, Joomla,... Đối với các dịch vụ cung cấp CMS (Content Management System) như vậy, tuy bản thân là open-source, nhưng các theme và template của chúng thì lại không. Do đó, ta không thể cá nhân hóa trang web 100% như mong muốn.

Khác với Dynamic Site, bao gồm cả server và client như trên, mình xin giới thiệu với các bạn **SSG - Static Site Generator**. Khi build một trang web cá nhân, một trang web "tĩnh" sẽ được ưu tiên hơn là một trang web động, nghĩa là sẽ không có database, không có log, có thể vẫn cho phép bình luận, nhưng bởi không có server-side nên sẽ không có real-time notification được trả về, v.v..

Dù không linh hoạt như một web động, web tĩnh vẫn được sử dụng khá rộng rãi là vì:
* Tốc độ : web tĩnh load rất nhanh, tất cả mọi thứ ở phía client đều đã được pre-built.
* Tùy biến : có thể custom design dễ dàng, chỉ cần chút HTML, CSS, và JavaScript cơ bản.
* Chi phí : không cần phải bảo trì hay quản lý một database phức tạp (bởi làm gì có database).
* Bảo mật : Vâng, chẳng ai đi hack một trang web tĩnh cả.

Tất nhiên chúng ta không build-from-scratch mà sẽ sử dụng những template có sẵn. Trong bài viết này, mình sẽ sử dụng framework **Hugo**. 
\
​
## 2. Cài đặt
Trước tiên, tải bản release mới nhất của Hugo tại [**đây**](https://github.com/gohugoio/hugo/releases/).

Sau khi giải nén, bạn sẽ nhận được một file hugo.exe, hãy thêm đường dẫn chứa file này vào PATH environment variables.

Sau khi thêm xong, ta check thử version của Hugo khi `cd` tại bất kỳ đâu trong terminal :
```bash
>>> hugo version
```
Nếu check thành công, vào việc.
\
​
### 2.1 Tạo Project
Mở VS Code, chúng ta sẽ tạo ra một folder qua lệnh dưới đây. Mình sẽ gọi nó là root folder (folder gốc):
```bash
>>> hugo new site tên_muốn_đặt_cho_root_folder
```
Bên trong, một vài folder rỗng đồng thời cũng được tạo ra, cũng là nơi ta sẽ đưa vào các nội dung, hình ảnh,... Mình sẽ lấp đầy chúng trong chốt lát.
\
​
### 2.2 Chọn Theme

Cùng chọn cho mình một theme tùy thích tại chợ  [**Themes**](https://themes.gohugo.io/) của Hugo.
\
\
Chẳng hạn, mình chọn theme Stack, các bạn có thể tham khảo theme này tại [**Sound Engineering**](https://kpnn0100.github.io), một static site của bạn mình cũng sử dụng framework này.

![](https://images.viblo.asia/5b9d5cbb-b2ee-4968-bc8b-c913e1374d9c.png)

Tùy vào theme sẽ có phần **Demo** (hoặc không) để các bạn xem thử, nếu ưng ý, chạy lệnh git sau tại root folder:


```bash
>>> cd themes
>>> git clone https://github.com/CaiJimmy/hugo-theme-stack.git


    cú pháp sẽ trông như dưới đây:
    git clone https://github.com/url_của_theme_trên_github.git  
```

\
Trường hợp khác, nếu mọi người không thể git được (như mình chẳng hạn 😶 do proxy công ty), chỉ việc tải trực tiếp folder zip của theme đó qua nút **Download** trong hình (hoặc tại repo).
\
\
​
### 2.3 Cấu trúc cơ bản của một Theme

Một theme (chủ đề), bao gồm nhiều thành phần như tone màu chủ đạo, menu, font chữ, kiểu bo góc,... đồng điệu với nhau.  
Ta cần chú ý đến một file gọi là file ⚙️config. Đây sẽ là file dùng để chỉnh sửa nhanh những gì nổi bật nhất của một theme.
> File config tồn tại dưới 3 đuôi khác nhau gồm `.toml` `.yaml` hoặc `.json` tuỳ vào sở thích của tác giả, nhưng chung quy lại chúng chỉ khác nhau về cú pháp mà thôi.

\
Dưới đây là cấu trúc cơ bản của file config.toml bên trong folder **📁exampleSite** (đã được mình lược bớt). Tùy vào nhu cầu hiển thị của bạn nên cứ vọc vạch đi nhé.


```json
baseURL = "https://example.org/"

# Tên theme nếu không giống tên folder theme thì sẽ không tìm được.
theme = "tên_folder_theme"

# Tiêu đề website
title = "Dũng đẹp trai"

# Mã ngôn ngữ theo ISO 639 ["en", "vi", "fr", "pl", ...]
languageCode = "en"

# Tên ngôn ngữ ["English", "Vietlam", "Français", "Polski", ...]
languageName = "English"

# Thông tin tác giả
[author]
  name = "tên"
  email = "meo"
  link = "linh"

# Menu: tương tự mục hình ảnh, video, bạn bè trên facebook.
[menu]
  [[menu.main]]
    weight = 1
    identifier = "posts"
    pre = ""
    post = ""
    name = "📜Bài viết" # hover vào name sẽ thấy title
    url = "/posts/"
    title = "Dũng"
  [[menu.main]]
    weight = 2
    identifier = "tags"
    pre = ""
    post = ""
    name = "🏷️Thẻ"
    url = "/tags/"
    title = "đẹp"
  [[menu.main]]
    weight = 3
    identifier = "categories"
    pre = ""
    post = ""
    name = "📁Mục"
    url = "/categories/"
    title = "trai"
```
\
\
\
​
### 2.4 Khởi chạy trên local
Ban nãy, khi bạn tạo ra các folder rỗng bên trong root folder, một file config cũng được tạo ra, nhớ thêm vào file này dòng `theme = 'tên_folder_theme'` nhé. Sau đó:
```bash
>>> hugo server
```
\
\
Truy cập vào `localhost:1313`.

![](https://images.viblo.asia/3beeaae9-5d4d-4b16-8ca6-22cf0492418d.png)

Oops, sao trống hoác thế này.
\
\
Để xem thử một website hoàn chỉnh, chúng ta sẽ trỏ sang  **📁exampleSite** (một subfoler bên trong theme các bạn vừa clone về), chính là trang web mà mọi người thấy khi nhấn vào nút **Demo** ban nãy. Thử lại nào:
```bash
>>> cd themes\tên_theme\exampleSite
>>> hugo server
```
\
Và..
​



![exampleSite của theme Stack](https://images.viblo.asia/9e419009-ec1e-4845-8655-7ea726ea9d08.png)



> `Thông thường, với mỗi file index.ngôn_ngữ.md bên trong thư mục posts (tượng trưng cho từng bài viết trên web), sẽ có một dòng lệnh như thế này `draft: false`. Nếu giá trị của nó là `true`, nghĩa là post đó đang được lưu ở dạng nháp, nó sẽ không hiện lên web.`

\
Do đó, nếu cảm thấy một vài post biến mất, ta có thể ép chúng xuất hiện bằng cách gõ lệnh dưới đây:
```bash
>>> hugo server -D
```
\
Tuy vậy, nếu muốn chúng luôn luôn xuất hiện sau khi đã deploy trang web hẳn hoi, nhớ vào code sửa lại thành `false` cho chắc kèo nhé.
\
​
## 3. Tùy chỉnh
### 3.1 Viết Blog thôi nào !
Trông thì cũng đẹp đấy, nhưng nếu chúng ta muốn viết content cho riêng mình thì phải làm thế nào ? Hiện tại ta đang ở **📁exampleSite**,  `cd` lùi lại 3 level để quay về root folder:
```bash
>>> cd ../../../
```
\
\
Trỏ vào **📁content**, tạo một vài subfolder và một file markdown :
```bash
>>> cd content
>>> mkdir posts
>>> mkdir tên_blog_muốn_đặt
>>> hugo new tên_file_markdown_muốn_đặt.md
```
\
\
\
\
\
Ơ mà khoan, markdown là gì cơ ?
\
\
\
\
​
### 3.2 Markdown

Ví dụ, mình mở một file .md bất kỳ theo đường dẫn dưới đây:
>**📁exampleSite**>**📁content**>**📁posts**>**📁tên_folder_bài_viết**>`index.ngôn_ngữ.md`
```json
---
weight: 1
title: "[HUGO] - Mình Có Một Thằng Mentor Hay Trốn Việc"

date: 2022-10-12T22:29:01+08:00
lastmod: 2022-15-06T21:29:01+08:00
draft: false
author: " Dũng Học Giỏi"
authorLink: "https://www.facebook.com/queo.stn/"
description: "!"

images: []
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["web", "tutorial"]
categories: ["tài liệu"]

lightgallery: true

toc:
  auto: false
---

Bên trên là phần tiêu đề, để viết nội dung thì chỉ cần tiếp tục viết thôi.
v.v..  NỘI DUNG  v.v..

```
\
Đây chính là file chứa toàn bộ nội dung của một bài viết. Mỗi khi nhấn vào một bài viết bất kỳ trên [**Dũng Học Giỏi**](https://du4ng.github.io), tất cả content mà bạn đọc được khi lăn chuột, đều được mình thủ công viết dưới dạng markdown, bao gồm cả table, hiệu ứng in đậm in nghiêng, các đề mục và cả đường link. Điều này tương tự cho các bài viết mà bạn đọc trên **Viblo**.
\
​
### 3.3 Custom theme
Nếu bạn muốn trùng tu cho trang web của mình, chỉ cần một chút kiến thức về `css`/`scss`.
Bên trong folder **📁themes** sẽ chứa một số subfolder quan trọng như:

|Folder     | Chứa các file  |
| ----------   | -----------           |
| assets    | CSS                  |
|                | SCSS                |
|                | JS                      |
| layouts  |HTML                |
| static     | font chữ           |
| i18n       | ngôn ngữ         |

\
Hoặc, bạn có thể inspect các element trên site để tìm thông tin của chúng dễ dàng hơn trong root folder.
\
​
### 3.4 Ngôn ngữ tương thích
Thông thường, các mục của một trang web có thể thay đổi được ngôn ngữ, riêng content thì tuỳ vào tác giả có dịch tay hay không.

Điều này có thể thực hiện bằng cách sử dụng các file `"ngôn_ngữ".toml` bên trong folder **i18n**.
\
\
\
​
## 4. Web Hosting 
Công đoạn cuối cùng, chúng ta sẽ đưa web lên server nhé.

### 4.1 Đưa web lên server

Chúng ta sẽ cần một server để host trang web. Có khá nhiều lựa chọn như GitHub, GitLab, Netlify, Firebase,... Trong bài viết lần này mình sẽ chọn GitHub.
\
\
GitHub cung cấp một tên miền miễn phí đối với mỗi user như sau :`tên_user.github.io`. Ta sẽ tạo một repo mới trên GitHub, đặt tên giống với tên miền trên. Ví dụ như [du4ng.github.io](https://github.com/Du4nG/du4ng.github.io)
\
\
​Tại root folder, gõ :
```bash
>>> hugo
```
\
Folder **📁public** sẽ được tạo ra, đây sẽ là nơi chứa toàn bộ những gì sẽ hiển thị trên server, được generate từ một số folder nhất định. Vì vậy, cấu trúc file sẽ khá khác với cấu trúc trên local.
\
\
Bước cuối cùng, chúng ta sẽ push mọi thứ bên trong folder này lên trên repo vừa tạo.  

```bash
>>> cd public
>>> git init
>>> git remote add origin https://github.com/tên_user/tên_user.github.io.git
>>> git add .
>>> git commit -m "first commit"
>>> git push origin master
```
\
Tất cả file bên trong **📁public** lúc này đã được đẩy lên repo. Chờ vài phút, trang web của các bạn sẽ xuất hiện khi ta nhập `tên_user.github.io` vào thanh URL trên trình duyệt.

\
\
​
### 4.2 Thay hình đổi dạng
Nhưng, dùng tên miền như vậy sẽ bị người khác đánh giá đấy. Có rất nhiều đơn vị cung cấp tên miền uy tín như Namecheap, GoDaddy, BlueHost,... Các bạn có thể tham khảo các đuôi phổ biến sau:
|Trả phí                                      | Miễn phí      |
| --------                                       | -----------         |
| .com .dev. org .edu .vn .net |.tk .cf .gq .ga .ml|

\
Apex domain mình từng dùng là *bbtd.tech* tại [**Hostinger**](https://www.hostinger.com) với phí ưu đãi chưa đến $1 cho năm đầu tiên, nhưng từ năm tiếp theo nó đã trở về hơn... $50. Hiện mình đã chuyển qua *bbtd.dev* với giá khoảng $15, các domain như .com, .ai sẽ có giá tương tự hoặc đắt hơn.

Nhưng trong bài viết này, mình sẽ chọn [**Freenom**](https://www.freenom.com) vì miễn phí và giao diện tại đây khá đơn giản. Chi tiết cách để tậu cho mình một tên miền qua bất kỳ đơn vị nào, các bạn có thể tra Google vì tùy đơn vị sẽ có cách đăng ký khác nhau.
\
\
Sau khi config xong xuôi trên Freenom các bạn hẳn tiếp tục với bước này nhé. Lấy ví dụ về tên miền mà GitHub cung cấp sẵn, ta thử truy vấn đến du4ng.github.io qua [**Dig**](https://toolbox.googleapps.com/apps/dig) - một DNS Lookupcủa Google. Kết quả trả về như sau:

![](https://images.viblo.asia/454ce83f-190f-4169-8a69-1d2462e25911.png)

\
Kết quả nhận được  là một bản ghi A (A Record) bao gồm bốn địa chỉ IP. Các địa chỉ này chính là IP của GitHub Pages, nơi mà trang web của các bạn đang được host. Mỗi lần các bạn gõ `tên_user.github.io` vào thanh URL của trình duyệt, tên miền này sẽ được phân giải thành một trong bốn IP trên, trỏ đến GitHub Pages của các bạn.

\
\
Chúng ta sẽ làm một động tác, tương tự như nguyên lý ban nãy, dùng custom domain để trỏ đến bốn địa chỉ IP. Ta sẽ modify tên miền trên Freenom, tiến hành nhập bốn địa chỉ vào bốn dòng tương ứng tại cột Target:


| 185.199.108.153| 
| -------- | 

|185.199.109.153| 
| -------- | 

|185.199.110.153| 
| -------- | 

|185.199.111.153| 
| -------- | 


![](https://images.viblo.asia/77796076-f15e-442a-8e89-3e089680ee3f.png)

\
\
Tại repo, tìm đến **⚙️Settings**, nhấn vào **Pages**:

![](https://images.viblo.asia/cc06aab1-cb20-4780-bfe7-d5e6c786402b.png)


Sau khi nhấn Save, một file **CNAME** (không đuôi) sẽ được tạo ngay trong repo, với nội dung chỉ vọn vẻn là tên miền custom.
\
\
Tại ô **Enforce HTTPS** (khoảng 24h sau mới tích được) nên các bạn cứ bình tĩnh. Thông thường, các đơn vị cung cấp tên miền miễn phí chỉ hỗ trợ HTTP, nên nếu bạn truy cập web từ Facebook thì có thể gặp filter cho insecure sites của Facebook đấy.
\
\
Và thế là hết !
\
\
​
## 5. Kết
Tương truyền rằng, Nguyen Dang Quang đang dần trở thành robot.