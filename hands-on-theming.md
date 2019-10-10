---
description: >-
  Bài viết được dựa theo tutoriral của Drupalize me
  https://drupalize.me/guide/hands-on-theming
---

# Hands-On Theming

## 1. Lời mở đầu:

Bài viết gồm 7 tuần , với mỗi tuần là một "keynote" của Drupal 8 theming . Với mỗi một week bạn sẽ được thực hành lại với exercise để củng cố lại kiến thức của mình. 

## 2. Bắt đầu một chặng đường mới: 

### A. Setup: 

Cách 1: Sử dụng composer để tạo một project Drupal mới

Cách đơn giản nhất để tạo một project với composer là sử dụng template command .  Khi bạn chạy  `composer create-project some/project`,nó sẽ clone `some/project` và sử dụng nó như một template mới của project drupal.

VD:

```text
$ composer create-project drupal-composer/drupal-project:8.x-dev my-project --stability dev --no-interaction
$ cd my-project
```

Bạn có thể tìm hiểu thêm  [`drupal-composer/drupal-project` documentation](https://github.com/drupal-composer/drupal-project) để biết thêm chi tiết.

#### Cài đặt một Drupal package thông qua Composer 

Để cài đặt drupal package, bạn phải chắc chắn mình đã có file composer.json  [Composer Configuration for Drupal](https://drupalize.me/tutorial/composer-configuration-drupal). 

Để install một  Drupal project \(module, theme, profile, etc.\), chạy lệnh:

```text
$ composer require drupal/[project]
```

Ví dụ  require `ctools`, chạy lệnh:

```text
$ composer require drupal/ctools
```

Mặc định , composer sẽ install bản latest version, bạn cũng có thể cài version cụ thể bằng cách:

```text
$ composer require drupal/ctools 1.0.0
```

#### Updating  dependency

Để  update package bất kỳ , chạy lệnh:

```text
composer update [vendor]/[package]
```

Ví dụ để update `drupal/ctools`, chạy lệnh:

```text
$ composer update drupal/ctools
```

Lưu ý rằng câu lệnh này chỉ  update **duy nhất** `drupal/ctools` và không update `drupal/ctools`'s dependencies.

Để update `drupal/ctools` và các dependency  `drupal/ctools  chạy lệnh`:

```text
$ composer update drupal/ctools --with-all-dependencies
```

Để update tất cả các package ,chạy lệnh:

```text
$ composer update
```

### B. Week 2: Create a New Theme

#### 1. Introduction YAML

 [**YAML**](https://vinasupport.com/tag/yaml/) \(YAML Ain’t Markup Language\) là một chuẩn dữ liệu kiểu serialization dành cho tất cả các ngôn ngữ. Nó được sử dụng phổ biến để tạo ra các file config cho nhiều ứng dụng, VD: như Docker Compose.

#### 2. Create an info file 

#### Chọn tên 

Ví dụ , tôi đặt theme của tôi là  _Ice Cream_ với machine name  _icecream_.

**Note:** Machine name tất cả phải là  lowercase,bắt đầu với một chữ cái , sử dụng  underscore \(_\) thay cho space và không chứa bất kỳ ký tự nào khác  .Ví dụ  \_icecream_, hoặc _ice\_cream_.

#### Create an info file

Tạo một file  file _themes/icecream/icecream.info.yml_

#### Chỉnh sửa info file

Mở _themes/icecream/icecream.info.yml_  và add nội dụng sau:

```text
# THEMENAME.info.yml file for Ice Cream example theme.
name: Ice Cream
type: theme
base theme: classy
description: 'A great theme for warm summer days.'
package: Custom
core: 8.x
```

Chi tiết:

**name** \(required\)  Tên của theme, hiển thị trong Drupal UI 

**type** \(required\)  Đặt là   'theme' nếu là  Theme.

**description** A short one-line description used in the UI when listing your theme.

**package** The package your theme belongs in; used for grouping projects together.

**core** \(required\) The version of Drupal core that your theme is compatible with. Required; for Drupal 8 themes this will likely always just be '8.x'.

**base theme** \(default = Stable\) The machine name of an installed theme to be used as a base theme. If no base theme is set, then the core base theme "Stable" will be used. Classy is the other base theme alternative provided in core. If no base theme should be used, enter "false" as a value for this key. \([Change record](https://www.drupal.org/node/2580687)\)

See a [complete list of keys](https://www.drupal.org/node/2349827) - all of which will be covered in future tutorials.

#### Clear the cache

With your _themes/iceream.info.yml_ file in place, Drupal should be able to recognize your theme and display it as an option on the _Appearance_ page. You just need to clear the cache by navigating to _Configuration_ &gt; _Performance_ \(admin/config/development/performance\) page and clicking the _Clear all caches_ button. This will cause Drupal to recreate the list of themes it knows about - and this time it will find your _.info.yml_ file and recognize your new theme.

#### Verify your theme is listed

Finally, navigate to the _Appearance_ \(admin/appearance\) page. You should see your Ice Cream theme listed under _Uninstalled themes_.

### 





