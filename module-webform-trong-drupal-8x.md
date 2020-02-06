# Module Webform trong Drupal 8x

## Giới thiệu về Webform

Webform là mô-đun để tạo các biểu mẫu và khảo sát trong Drupal. Sau khi gửi e-mail có thể tùy chỉnh có thể được gửi đến quản trị viên và / hoặc người gửi. Kết quả có thể được xuất sang Excel hoặc các ứng dụng bảng tính khác. Webform cũng cung cấp một số đánh giá thống kê cơ bản và có API mở rộng để mở rộng các tính năng của nó.



## Installing the [Webform Module](https://www.drupal.org/project/webform)

Copy/upload the webform module to the modules directory of your Drupal installation.

* Enable the 'Webform' module and desired sub-modules in 'Extend'. \(/admin/modules\)
* Set up user permissions. \(/admin/people/permissions\#module-webform\)
* Build a new webform \(/admin/structure/webform\) or duplicate an existing template \(/admin/structure/webform/templates\).
* Publish your webform as a:
  * **Page:** By linking to the published webform. \(/webform/contact\)
  * **Node:** By creating a new node that references the webform. \(/node/add/webform\)
  * **Block:** By placing a Webform block on your site. \(/admin/structure/block\)
* \(optional\) Install third party libraries\(/admin/help/webform\).
* \(optional\) Install add-on contrib modules\]\(/admin/structure/webform/addons\).

## Webform Features

Webform module cho phép bạn có thể build bất cứ loại form nào mà có thể thu thập nhiều loại data, nơi mà có thể submit vào nhiều form hoặc hệ thống. Mỗi một behavior của form của bạn và dữ liệu đầu vào đều có thể customize được . Khi bạn cần một multi-page form chứa nhiều cột với điều kiện logic hoặc simple contact form có thể đẩy dữ liệu vào SalesForce/CRM thì bạn có thể sử dụng tất cả nó ở trong webform module dành cho Drupal 8.

Drupal và mô-đun Webform cố gắng truy cập đầy đủ cho tất cả người dùng và người xây dựng trang web. Các công nghệ hỗ trợ, bao gồm screen readers và keyboard access, được hỗ trợ đầy đủ.



### Form manager <a id="s-form-manager"></a>

| [![Form manager](https://www.drupal.org/files/webform-8.x.5.x-features--form-manager.png) **Form manager**](https://www.drupal.org/files/webform-8.x.5.x-features--form-manager.png) | [![ Add webform](https://www.drupal.org/files/webform-8.x.5.x-features--form-manager-add.png) **Add webform**](https://www.drupal.org/files/webform-8.x.5.x-features--form-manager-add.png) |
| :--- | :--- |


Trình quản lý biểu mẫu cung cấp một danh sách tất cả các biểu mẫu web có sẵn. 

Các tính năng của trình quản lý biểu mẫu bao gồm: 

* Lọc theo từ khóa, danh mục và trạng thái 
* Sắp xếp theo tổng số bài nộp
*  Lưu trữ các hình thức cũ

### Form builder <a id="s-form-builder"></a>

| [![Form builder](https://www.drupal.org/files/webform-8.x.5.x-features--form-builder.png) **Form builder**](https://www.drupal.org/files/webform-8.x.5.x-features--form-builder.png) | [![Edit element](https://www.drupal.org/files/webform-8.x.5.x-features--form-builder.png) **Edit element**](https://www.drupal.org/files/webform-8.x.5.x-features--form-builder.png) |
| :--- | :--- |


Mô-đun Webform cung cấp trình tạo biểu mẫu trực quan dựa trên các thực tiễn tốt nhất của Drupal 8 cho thiết kế giao diện người dùng và trải nghiệm người dùng. Trình tạo biểu mẫu cho phép người dùng không có kỹ thuật dễ dàng xây dựng và duy trì biểu mẫu web.

Các tính năng xây dựng biểu mẫu bao gồm:

* Drag-n-drop form element management
* Multi-column layout management
* Conditional logic overview
* Element duplication

### Configuration settings <a id="s-configuration-settings"></a>

Hành vi biểu mẫu, tính năng, xử lý gửi, nhắn tin và xác nhận hoàn toàn có thể tùy chỉnh bằng cách sử dụng cài đặt chung và / hoặc cài đặt dành riêng cho biểu mẫu.

| [![ General](https://www.drupal.org/files/webform-8.x.5.x-features--settings-general.png) **General**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-general.png) | [![ Form](https://www.drupal.org/files/webform-8.x.5.x-features--settings-form.png) **Form**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-form.png) |
| :--- | :--- |


#### General settings <a id="s-general-settings"></a>

Cho phép thông tin quản trị, đường dẫn, hành vi và cài đặt của bên thứ ba được tùy chỉnh.

General settings include:

* Categorization
* Customizable paths
* Disable saving of results
* Ajax support

#### Form settings <a id="s-form-settings"></a>

Cho phép trạng thái, thuộc tính, hành vi, nhãn, thông báo, cài đặt trình hướng dẫn và xem trước của biểu mẫu được tùy chỉnh.

Form settings include:

* Open and close date/time scheduling
* Login redirection with custom messaging.
* Multiple step wizard forms
* Submission preview
* Input prepopulation using query string parameters.

| [![ Submisssions](https://www.drupal.org/files/webform-8.x.5.x-features--settings-submissions.png) **Submisssions**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-submissions.png) | [![ Confirmation](https://www.drupal.org/files/webform-8.x.5.x-features--settings-confirmation.png) **Confirmation**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-confirmation.png) |
| :--- | :--- |


#### Submissions settings <a id="s-submissions-settings"></a>

Cho phép nhãn, hành vi, giới hạn và cài đặt dự thảo được gửi tùy chỉnh.

Submission settings bao gồm:

* Saving of drafts
* Automatic purging of submissions
* Submission limits per user and/or per form
* Autofilling form using previously submitted values

#### Confirmation settings <a id="s-confirmation-settings"></a>

Cho phép loại xác nhận, thông báo và URL của biểu mẫu được tùy chỉnh.

Confirmation types bao gồm :

* Dedicated page
* Redirect to internal or external URL
* Displaying of a custom status message
* Opening a modal dialog

| [![ Handlers](https://www.drupal.org/files/webform-8.x.5.x-features--settings-handlers.png) **Handlers**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-handlers.png) | [![ Email handler](https://www.drupal.org/files/webform-8.x.5.x-features--settings-handlers-email.png) **Email handler**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-handlers-email.png) |
| :--- | :--- |


#### Emails / Handlers <a id="s-emails-handlers"></a>

Cho phép các hành động và hành vi bổ sung được xử lý khi biểu mẫu web hoặc nội dung gửi được tạo, cập nhật hoặc xóa. Trình xử lý được sử dụng để định tuyến dữ liệu đã gửi đến các ứng dụng bên ngoài và gửi thông báo & xác nhận.

Email support features bao gồm :

* Previewing and resending emails
* Sending HTML emails
* File attachments \(requires the Mail System and Swift Mailer module.\)
* HTML and plain-text email-friendly Twig templates
* Customizable display formats for individual form elements

Các tính năng của bài đăng từ xa bao gồm: - Đăng các phần tử được chọn lên máy chủ từ xa - Thêm tham số tùy chỉnh vào yêu cầu bài đăng từ xa

| [![ CSS/JS assets](https://www.drupal.org/files/webform-8.x.5.x-features--settings-assets.png) **CSS/JS assets**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-assets.png) | [![ Access](https://www.drupal.org/files/webform-8.x.5.x-features--settings-access.png) **Access**](https://www.drupal.org/files/webform-8.x.5.x-features--settings-access.png) |
| :--- | :--- |


#### CSS/JS assets <a id="s-cssjs-assets"></a>

Trang assert  CSS / JS cho phép người xây dựng trang web đính kèm CSS và JavaScript tùy chỉnh vào biểu mẫu web. CSS tùy chỉnh có thể được sử dụng để thực hiện bố cục đơn giản hoặc điều chỉnh thiết kế thành một biểu mẫu. JavaScript tùy chỉnh cho phép bổ sung logic và hành vi có điều kiện vào một biểu mẫu.

#### Access settings <a id="s-access-settings"></a>

Cho phép quản trị viên xác định ai có thể quản trị biểu mẫu web và / hoặc tạo, cập nhật, xóa và xóa nội dung gửi biểu mẫu web.

### Elements <a id="s-elements"></a>

| [![Elements](https://www.drupal.org/files/webform-8.x.5.x-features--elements.png) **Elements**](https://www.drupal.org/files/webform-8.x.5.x-features--elements.png) | [![Element settings](https://www.drupal.org/files/webform-8.x.5.x-features--elements-settings.png) **Element settings**](https://www.drupal.org/files/webform-8.x.5.x-features--elements-settings.png) |
| :--- | :--- |


The Webform module is built directly on top of Drupal 8's Form API. Every form element available in Drupal 8 is supported by the Webform module.

Form elements include:

* **Basic HTML**: Textfield, Textareas, Checkboxes, Radios, Select menu, Password, and more...
* **Advanced HTML5**: Email, Url, Number, Telephone, Date, Number, Range, and more...
* **Advanced Drupal**: File uploads, Entity References, Table select, Date list, and more...
* **Widgets**: Likert scale, Star rating, Buttons, Geolocation, Terms of service, Select/Checkboxes/Radios with other, and more...
* **Markup**: Dismissible messages, Basic HTML, Advanced HTML, Details, and Fieldsets.
* **Composites**: Name, Address, Contact, Credit Card, and event custom composites
* **Computed**: Calculated values using Tokens and Twig with Ajax support.

#### Element settings <a id="s-element-settings"></a>

All of Drupal 8's default form element properties and behaviors are supported. There are also several custom webform element properties and settings available to enhance a form element's behavior.

Standard and custom properties allow for:

* Customizable error validation messages
* Conditional logic using [FAPI States API](https://api.drupal.org/api/examples/form_example%21form_example_states.inc/function/form_example_states_form/7)
* Input masks \(using [jquery.inputmask](https://github.com/RobinHerbots/jquery.inputmask)\)
* [Select2](https://select2.github.io/) or [Chosen](https://harvesthq.github.io/chosen/) replacement of select boxes
* Word and character counting for text elements
* Help tooltips \(using [jQuery UI Tooltip](https://jqueryui.com/tooltip/)\)
* More information slideouts
* Regular expression pattern validation
* Private elements, visible only to administrators
* Unique values per element

| [![Conditional logic](https://www.drupal.org/files/webform-8.x.5.x-features--elements-conditional.png) **Conditional logic**](https://www.drupal.org/files/webform-8.x.5.x-features--elements-conditional.png) | [![View source](https://www.drupal.org/files/webform-8.x.5.x-features--elements-source.png) **View source**](https://www.drupal.org/files/webform-8.x.5.x-features--elements-source.png) |
| :--- | :--- |


#### States/Conditional logic <a id="s-statesconditional-logic"></a>

Drupal's State API can be used by developers to provide conditional logic to hide and show form elements.

Drupal's State API supports:

* Show/Hide
* Required/Optional
* Open/Close
* Enable/Disable

#### Viewing source <a id="s-viewing-source"></a>

At the heart of a Webform module's form elements is a Drupal [render array](https://www.drupal.org/docs/8/api/render-api/render-arrays), which can be edited and managed by developers. The Drupal render array gives developers complete control over a webform's elements, layout, and look-and-feel by allowing developers to make bulk updates to a webform's label, descriptions, and behaviors.

### Forms <a id="s-forms"></a>

| [![Accessibility](https://www.drupal.org/files/webform-8.x.5.x-features--forms-accessiblity.png) **Accessibility**](https://www.drupal.org/files/webform-8.x.5.x-features--forms-accessiblity.png) | [![Multistep form](https://www.drupal.org/files/webform-8.x.5.x-features--forms-wizard.png) **Multistep form**](https://www.drupal.org/files/webform-8.x.5.x-features--forms-wizard.png) |
| :--- | :--- |


#### Accessibility <a id="s-accessibility"></a>

The outputted forms and even the Webform module's administrative interface \(i.e. form builder\) are accessible using keyboard navigation and screen readers. The Webform module complies with [WCAG 2.0](http://www.w3.org/TR/WCAG20/#contents) and [ATAG 2.0](http://www.w3.org/TR/ATAG20/#contents) guidelines.

#### Multistep form <a id="s-multistep-form"></a>

Forms can be broken up into multiple pages using a progress bar. Authenticated users can save drafts and/or have their changes automatically saved as they progress through a long form.

Multistep form features include:

* Customizable progress bar
* Customizable previous and next button labels and styles
* Saving drafts between steps

#### Drupal integration​ <a id="s-drupal-integration"></a>

| [![Block](https://www.drupal.org/files/webform-8.x.5.x-features--forms-block.png) **Block**](https://www.drupal.org/files/webform-8.x.5.x-features--forms-block.png) | [![Node](https://www.drupal.org/files/webform-8.x.5.x-features--forms-node.png) **Node**](https://www.drupal.org/files/webform-8.x.5.x-features--forms-node.png) |
| :--- | :--- |


Các biểu mẫu web có thể được gắn vào các nút hoặc hiển thị dưới dạng các khối. Các biểu mẫu web cũng có thể có các URL thân thiện với SEO chuyên dụng. Các phần tử biểu mẫu là các mảng kết xuất có thể dễ dàng được thay đổi bằng cách sử dụng các móc và / hoặc plugin tùy chỉnh.

### Results management <a id="s-results-management"></a>

| [![Results](https://www.drupal.org/files/webform-8.x.5.x-features--results.png) **Results**](https://www.drupal.org/files/webform-8.x.5.x-features--results.png) | [![Customize results](https://www.drupal.org/files/webform-8.x.5.x-features--results-customize.png) **Customize results**](https://www.drupal.org/files/webform-8.x.5.x-features--results-customize.png) |
| :--- | :--- |


Việc gửi biểu mẫu có thể tùy chọn được lưu trữ trong cơ sở dữ liệu, được xem xét và tải xuống. Đệ trình cũng có thể được gắn cờ với ghi chú hành chính.

Results management features bao gồm:

* Submission flagging, locking, and notes
* Viewing submissions as HTML, plain text, and YAML
* Customizable reports
* Downloading results as a CSV to Google Sheets or MS Excel
* Saving of download preferences per form
* [Drupal Views](https://www.drupal.org/docs/8/core/modules/views) integration for advanced reporting.

### Access controls <a id="s-access-controls"></a>

| [![Permissions](https://www.drupal.org/files/webform-8.x.5.x-features--access-permissions.png) **Permissions**](https://www.drupal.org/files/webform-8.x.5.x-features--access-permissions.png) | [![Element access](https://www.drupal.org/files/webform-8.x.5.x-features--access-element.png) **Element access**](https://www.drupal.org/files/webform-8.x.5.x-features--access-element.png) |
| :--- | :--- |


Mô-đun Webform cung cấp các điều khiển và quyền truy cập đầy đủ để quản lý những người có thể tạo biểu mẫu, gửi bài và truy cập kết quả của biểu mẫu web. Kiểm soát truy cập có thể được áp dụng cho vai trò và / hoặc người dùng cụ thể. Mô hình con truy cập Webform cho phép bạn thậm chí thiết lập các nhóm quyền có thể sử dụng lại có thể được áp dụng cho nhiều phiên bản của cùng một biểu mẫu web.

Access controls cho phép users làm :

* Create new forms
* Update forms
* Delete forms
* View submissions
* Update submissions
* Delete submissions
* View selected elements
* Update selected elements

### Reusable templates <a id="s-reusable-templates"></a>

| [![Templates](https://www.drupal.org/files/webform-8.x.5.x-features--templates.png) **Templates**](https://www.drupal.org/files/webform-8.x.5.x-features--templates.png) | [![Templates preview](https://www.drupal.org/files/webform-8.x.5.x-features--templates-preview.png) **Templates preview**](https://www.drupal.org/files/webform-8.x.5.x-features--templates-preview.png) |
| :--- | :--- |


Mô-đun Webform cung cấp một vài mẫu khởi động và nhiều mẫu ví dụ mà quản trị viên biểu mẫu web có thể cập nhật hoặc sử dụng để tạo các mẫu có thể sử dụng lại mới cho tổ chức của họ.

Starter templates include:

* Contact Us
* Donation
* Employee Evaluation
* Issue
* Job Application
* Job Seeker Profile
* Registration
* Session Evaluation
* Subscribe
* User Profile

### Reusable options <a id="s-reusable-options"></a>

| [![Options](https://www.drupal.org/files/webform-8.x.5.x-features--options.png) **Options**](https://www.drupal.org/files/webform-8.x.5.x-features--options.png) | [![Likert](https://www.drupal.org/files/webform-8.x.5.x-features--options-likert.png) **Likert**](https://www.drupal.org/files/webform-8.x.5.x-features--options-likert.png) |
| :--- | :--- |


Quản trị viên có thể xác định các tùy chọn toàn cầu có thể sử dụng lại cho các menu, hộp kiểm và nút radio được chọn. Mô-đun Webform bao gồm các tùy chọn mặc định cho các tiểu bang, quốc gia, nhân khẩu học, câu trả lời thích, v.v.

Reusable options include:

* **Geographic**: Languages, country, and states
* **Date and time**: Days, months, and time zones
* **Demographic**: Education, employment status, ethnicity, Industry, languages, marital status, relationship, size, and job titles
* **Likert**: Agreement, comparison, importance, quality, satisfaction, ten scale, and would you

### Internationalization <a id="s-internationalization"></a>

Các biểu mẫu và cấu hình có thể được dịch sang nhiều ngôn ngữ bằng\[configuration translation system\]\([https://www.drupal.org/docs/8/core/modules/config-translation](https://www.drupal.org/docs/8/core/modules/config-translation).

### Add-ons <a id="s-add-ons"></a>

| [![Add-ons](https://www.drupal.org/files/webform-8.x.5.x-features--addons.png) **Add-ons**](https://www.drupal.org/files/webform-8.x.5.x-features--addons.png) | [![Analysis](https://www.drupal.org/files/webform-8.x.5.x-features--addons-webform-analysis.png) **Analysis**](https://www.drupal.org/files/webform-8.x.5.x-features--addons-webform-analysis.png) |
| :--- | :--- |


Có hàng tá tiện ích bổ sung có sẵn mở rộng và / hoặc cung cấp chức năng bổ sung cho mô-đun Webform và API biểu mẫu của Drupal.

Add-ons bao gồm :

* Analysis for creating graphs and charts
* CRM integration including SalesForce, HubSpot, MyEmma, SugarCRM, more…
* SPAM protection
* Advanced workflows
* Data encryption
* GDPR compliance

### Development tools <a id="s-development-tools"></a>

| [![Test](https://www.drupal.org/files/webform-8.x.5.x-features--devel-test.png) **Test**](https://www.drupal.org/files/webform-8.x.5.x-features--devel-test.png) | [![API](https://www.drupal.org/files/webform-8.x.5.x-features--devel-api.png) **API**](https://www.drupal.org/files/webform-8.x.5.x-features--devel-api.png) |
| :--- | :--- |


Các ví dụ và công cụ được cung cấp để giúp các nhà phát triển bắt đầu tùy chỉnh các tính năng hiện có và thêm các tính năng mới vào mô-đun Webform.

 Các công cụ phát triển bao gồm: 



* Các hình thức kiểm tra sử dụng các giá trị mặc định có thể tùy chỉnh
* Dễ dàng xuất tập tin cấu hình
*  Công cụ sửa lỗi cho tất cả các trình xử lý 
* Ví dụ về tích hợp API bên ngoài bằng cách sử dụng bài đăng từ xa hoặc mã tùy chỉnh 
* Các mô-đun ví dụ để tạo các phần tử và trình xử lý tùy chỉnh 
* Trình diễn xây dựng hệ thống đánh giá ứng dụng và đăng ký sự kiện

### Drush & Composer integration <a id="s-drush-composer-integration"></a>

| [![Drush](https://www.drupal.org/files/webform-8.x.5.x-features--drush.png) **Drush**](https://www.drupal.org/files/webform-8.x.5.x-features--drush.png) | [![Composer](https://www.drupal.org/files/webform-8.x.5.x-features--drush-composer.png) **Composer**](https://www.drupal.org/files/webform-8.x.5.x-features--drush-composer.png) |
| :--- | :--- |


Các lệnh Drush được cung cấp để:

* Generate multiple submissions
* Export submissions
* Purge submissions
* Download and manage third-party libraries
* Generate a composer.js file for third-party libraries
* Tidy YAML configuration files







