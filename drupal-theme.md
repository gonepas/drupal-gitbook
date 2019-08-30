---
description: Tìm hiểu về theme trong Drupal
---

# Drupal Theme

### Cấu trúc thư mục trong folder theme

```text
| cmc_theme.info.yml
| cmc_theme.theme
| cmc_theme.libraries.yml
| favicon.ico
| images
|  | - images.png
| css
|  | - tên_file_css_1.css
|  | - tên_file_css_2.css
| js
|  | - tên_file_js_1.js
|  | - tên_file_js_2.js
| templates
|  | - html.html.twig
|  | - page.html.twig
|  | - node.html.twig
|  | - maintenance-page.html.twig
```

{% hint style="info" %}
Chú thích:

cmc\_theme.info.yml: File thông tin của theme

cmc\_theme.theme: File khai báo các hàm hook\(\) của theme

cmc\_theme.libraries.yml: File khai báo các thư viện libraries

images: Folder chứa ảnh

css: Folder chứa các file css

js: Folder chứa các file js

templates: Folder chứa các file template của theme \(html.html.twig, page.html.twig...\)
{% endhint %}

### Tạo folder theme

Tạo mới folder, đặt tên folder. Đây sẽ là machine\_name của theme

VD trong hình sẽ là theme "cmc\_theme"

Truy cập folder "themes", tạo folder "custom", sau đó đặt folder "cmc\_theme" vào trong đây

![](.gitbook/assets/picture1%20%281%29.png)

### Tạo file khai báo để sử dụng theme

Trong folder "cmc\_theme" tạo file "cmc\_theme.info.yml"

Edit file với các thông số sau và lưu lại

```text
name: CMC Theme
type: theme
description: 'A custom theme of CMC.'
core: 8.x
logo: default_logo.png
screenshot: cmc_theme.png
libraries:
  - cmc_theme/global-styling
  - cmc_theme/global-scripts
regions:
  header: Header
  site_menu: Site Menu
  content: Main Content
  sidebar_left: Sidebar Left
  sidebar_right: Sidebar Right
  bottom_page: Page Bottom
  footer: Footer
```

{% hint style="info" %}
Chú thích

name: Tên của theme

description: Mô tả theme

core: Version drupal hiện tại

logo: Logo mặc định của theme

screenshot: Ảnh preview mặc định của theme

libraries: Khai báo các thư viện libraries

regions: Khai báo các vùng để sử dụng trong file page.html.twig
{% endhint %}

### Thêm file css và js vào theme

Sửa file "cmc\_theme.libraries.yml"

```text
global-styling:
  css:
    theme:
      css/tên_file_css_1.css {}
      css/tên_file_css_2.css {}
global-scripts:
  js:
    js/tên_file_js_1.js {}
    js/tên_file_js_2.js {}
dependencies:
  - core/jquery
```

### Twig trong Drupal 8

Drupal 8 sử dụng Twig Template Engine để thay cho cho PHPTemplate đã cũ trên Drupal 7. Vì vậy các syntax PHP cũ đã được thay thế trên Twig

Tham khảo thêm về TWIG: [https://twig.symfony.com/doc/1.x/templates.html](https://twig.symfony.com/doc/1.x/templates.html)

Theming Twig trong Drupal 8: [https://www.drupal.org/docs/8/theming/twig/twig-template-naming-conventions](https://www.drupal.org/docs/8/theming/twig/twig-template-naming-conventions)

### Debug trong Twig

Mở file "sites/default/services.yml"

Set các giá trị như ô bên dưới

```text
parameters:
  twig.config:
    debug: true
    auto_reload: true
```

Xóa cache trên Drupal

Mở Chrome, bấm F12 để hiển thị "View page source"

Click vào phần Setting của Inspect, tích chọn "Show HTML Comment"

### Theme hook suggestions

Các hàm hook\(\) theme hay sử dụng trong file "cmc\_theme.theme"

{% hint style="info" %}
hook\_theme: Hàm xử lý theme

hook\_preprocess\_html: Hàm xử lý html.html.twig

hook\_preprocess\_page: Hàm xử lý file page.html.twig

hook\_preprocess\_node: Hàm xử lý file node.html.twig

hook\_preprocess\_form: Hàm xử lý file form
{% endhint %}

