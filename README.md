# Cấu trúc khóa học trên Drupalize.me



### Drupal8 User Guide

[https://drupalize.me/guide/drupal-8-user-guide](https://drupalize.me/guide/drupal-8-user-guide)

* **Chapter 1:Hiểu về Drupal:** 1.Drupal là Cms 2.Modules của drupal.:cài, sử dụng và gỡ module 3.Theme của Drupal 4.Distributions của Drupal 5.các loại dữ liệu. -content:\(text,image,...vv\) . -configuration:dùng để cài đặt cho web site, cấu hình nên website -state:trang thái hiện tại của trang web, lưu trạng thái cron chạy lần cuối -session:lưu phiên đăng nhập của trang web 6..dự án drupal 7.điều khoản sử dụng Drupal
* **Chapter 2:Thiết lâp trang web :** 1.Region\(vùng\). 2.Site Layout\(bố trí điều hướng trang web\):Xác định điều hướng trang web như HomePage,Trang About… 3.Content Entities và Fields :bao gồm các loại sau: \* Content Entities: -content item:thực thể là nội dung được thể hiện chính trên trang web. -comment:”Bình luận”, trong một blog , người đọc có thể “bình luận” , đây chính là chức năng của comment. -User profile:Lưu dữ liệu người dùng, người đã có tài khoản trên trang web. -Custom block: văn bản, hình ảnh được chia thành các khối, giúp đặt vào các region. -Taxonomy Term:Phân loại nội dung, nội dung sẽ được phân theo loại, -File: ảnh, file được đính kèm trên trang web. -Contact Form:Form để người sử dụng có thể liên lạc với chủ trang web. \* Field: Trong mỗi content Entities lại có nhiều Field, mỗi field lưu một kiểu dữ liệu như ảnh, file, text, ngày tháng.. 4.Modular content. 5.Content Structure \(cấu trúc các content\):Học cách tổ chức các field, thêm mới các fileds sao cho cấu thành một content type đáp ứng yêu cầu.

6.workfkow: quy trình làm việc của trang web, quy cách phân quyền, thêm , xóa , sửa nội dung.  
7.Cấu hình ngôn ngữ cho trang web.

* **Chapter 3:Cài đặt** 1.yêu cầu máy chủ. 2. Giới thiệu một số công cụ\(Tool\) :Git ,Composer,Devel. 3.Tải và cài đặt Drupal 4.Chuẩn bị trước khi cài đặt. 5.Hướng dẫn sử dụng composer quản lý tải và cập nhật file. 6.Tải bản tải về thủ công. 7.Hướng dẫn cài đặt Drupal.



### Theme Drupal Site

[https://drupalize.me/guide/theme-drupal-sites](https://drupalize.me/guide/theme-drupal-sites)

#### A.Kiến thức căn bản.

* Giới thiệu chung 1.Theme là gì? Là làm cho giao diện một trang web có sự đồng nhất về một quy tắc giao diện, thể hiện nhât quán chung. 2.Cách cài đặ và gỡ cài đặt giao diện. 3.Cấu trúc của một giao diện : cách tổ chức các tập tin và thư mục cho theme. 4.Sử dụng Info file để khai báo một theme. 5.Nhanh theo mặc định: sử dụng cache. 6.Regions : Cấu hình regions cho trang web, học cách bố trí regions cho trang web bằng twig file. 7.Thêm Region cho theme: sử dụng file info , giao diện UI và twig file cấu hình vùng cho web.
* Cài đặt cho theme: 1.Tổng quan cài đặt theme. 2.Thay đổi cài đặt theme: cách cấu hình giao diện bằng UI. 3.Thêm ảnh chụp vào theme. 4.Giới thiệu core theme : Bartik
* Kế thừa theme: 1.Khái niệm kế thừa giao diện. 2.Kế thừa giao diện: ổn định và tốt 3.Sử dụng Base Theme.
* Giới thiệu template File 1.Thế nào là template File. 2.Ghi đè template file. 4.Xem Base Name của template. 5.Thiết kế template file với twig.
* Develeopment và Debug: 1.Cấu hình môi trường dể debug:  1.1 cấu hình vô hiệu hóa cache js/css  1.2 . Bật Twig Debug  1.3. Cài đặt PHP.  1.4.Một số tool debug\(kint và dump\)  1.5 XDebug. 2.Giới thiệu core theme :Stark. 3.Cách xóa cache trong Drupal  3.1.admin/config/development/performance \(sử dụng tool\)  3.2 xóa bằng drupal console 4.Kiểm tra biến trong twig template
* Suggest hook của theme 1.Khám phá các hook suggestion 2.Thêm mới Hook suggestions 
* Thư viện css và Java script 1.Khái niệm. 2.Khái báo thư viện assert library.khai báo các thư viện lên theme.libraries.yml 3.Đính kèm thư viện: sử dụng [hook\_page\_attachments\_alter](https://api.drupal.org/hook_page_attachments_alter) 
* Javascript trong Drupal: 1.Javascript trong drupal:Jquery,CKEditor,Modernizr,Picturefill, Backbone.js và UnderScore.js 2.Load JavaScript với Drupal.behaviors

4.Bọc code JavaScript trong Closure\(khung đóng\):

5. Drupal Settings phía máy chủ cho js:

core.libraries.yml  
truyền dữ liệu từ máy chủ sang máy khách, cung cấp thông tin cho js

### B.Kiến thức nâng cao

* Sử dụng React kết hợp với Drupal 1.Giới thiệu React và Drupal:React là một thư viện Java script, phần này chỉ ra cách React và Drupal có thể liên lạc với nhau 2.React cơ bản:Học React thông qua link đính kèm.

3.  
4.Kết nối React với Drupal Theme: cách cấu hình file và cáu hình trên site để kết nối React vói Drupal theme  
5.Tạo một React Component:React component chính là thành phần cơ bản để xây dựng một ứng dụng sử dụng react.  
6.Cấu hình Drupal để cung cấp dữ liệu qua JSON API

7.Cách nhận dữ liệu từ API với React

8.Thực hành Show danh sách dữ liệu từ Drupal bằng React

9.Thêm, xóa , sửa Node với React

10.Xây dựng một ứng dụng

11 xây dựng một ứng dụng đầy đủ  
12 Bảo mật OAuth với API Request  
13.Sử dụng Featch và OAuth để tạo bảo mật

14.Kế thừa với Google Material UI: Sử dụng Google Material UI để phát triển ứng dụng

