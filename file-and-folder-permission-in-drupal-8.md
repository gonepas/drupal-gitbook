---
description: Phân quyền thư mục trong drupal 8
---

# File and folder permission in drupal

### 1. Tại sao cần đến permission trong drupal 

Để nâng cao tính bảo mật và sử dụng tài nguyên 1 cách hiệu quả

### 2. Các quyền thư mục trong drupal được khuyến nghị set như sau 

* all files permission 444
* all directory permission 555
* root 'htdocs' directory permission 555
* sites/default/files directory permission 775
* all directories in sites/default/files 775
* all files in sites/default/files 664
* sites/default/settings.php permission 444
* không nên đặt thư mục tmp tại thư mục drupal root, đặt tmp bên ngoài khu vực mà hacker có thể truy cập thông qua web url

### 3. Cách thiết lập permission trong drupal

Để thao tác với file và folder ta cần cấp các quyền truy cập để đọc \(r\), ghi \(w\) và thực thi \(x\) tương ứng

#### 3.1. Setting Drupal File Permissions sử dụng FTP

**For Directories**

* Đối với tất cả các thư mục, set permission 775
* Các bước setting sử dụng FPT

1. Log into vào tài khoản FTP
2. Điều hướng đến thư mục Drupal được cài đặt Ex: \(/path/to/your/drupal/install/\)
3. Click chuột phải vào thư mục Drupal đã được cài đặt. Click vào option File Permissions trên menu
4. Khi click vào option, một cửa sổ mới được mở ra. Ở trường nhập giá trị, nhập giá trị "775"
5. Click enable Recurse vào tùy chọn sub-directories. Ở màn hình bên dưới, chọn checkbox có title “Apply to directories only”
6. Khi đã sẵn sàng, click button OK
7. Quá trình này có thể mất vài phút cho một lượng lớn tệp tin

**For Files**

* Đối với tất cả các file, set permission 640
* Các bước setting

1. Click chuột phải vào thư mục Drupal đã được cài đặt. Click vào option File Permissions trên menu
2. Khi click vào option, một cửa sổ mới được mở ra. Ở trường nhập giá trị, nhập giá trị "640**"**
3. Click enable Recurse vào tùy chọn sub-directories. Ở màn hình bên dưới, chọn checkbox có title “Apply to files only”
4. Khi đã sẵn sàng, click button OK
5. Quá trình này có thể mất vài phút cho một lượng lớn tệp tin

#### 3.2. Setting permissions sử dụng command

**For Directories**

Sử dụng command

**ls -al**

_**drwxr-xr-x**_

**For Files**

Sử dụng command

**ls -al**

**-rw-r–r–**

