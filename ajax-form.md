# Ajax Form

## Overview

Thêm event ajax callback vào trường của form để có thể update fields hoặc thêm markup, để người dùng có thể tương tác với form.

#### Ajax callback function có thể sử dụng để :

* Có thể update hoặc thêm mới fields của form
* Update giá trị của fields
* Chạy các hàm tiền xử lý ajax hặc có thể chạy code Javascript

Nếu bạn muốn tạo các ràng buộc fields, ẩn hiện dựa vào fields khác , bạn có thể tham khảo   [Form API \#states property](https://www.drupal.org/docs/8/api/form-api/conditional-form-fields).

#### Các bước để sử dụng Ajax trong form của Drupal



1. Tạo ra một form mới hoặc sử dụng hàm [hook\_form\_alter](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Form%21form.api.php/function/hook_form_alter) để thay đổi một form có sẵn 
2. Thêm '\#ajax' khi render element của field sẽ dùng trong hàm callback
3. Thực hiện đặt tên của hàm callback và loại event sẽ thực hiện.
4. Khi mà sự kiện thay đổi giá trị của fields form,hàm callback sẽ được gọi.
5. Hàm allback sẽ cho phép truy cập $form array và  FormstateInterface và cuối cùng phải returm array hoặc html markup hoặc dùng [AJAX Command](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Ajax%21CommandInterface.php/interface/implements/CommandInterface).

## Ví dụ với Drupal Ajax Form







####  

