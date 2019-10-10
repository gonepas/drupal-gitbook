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

**description**  Một dòng description ngắn sử dụng trong UI khi listing theme

**package** The package mà theme của bạn thuộc về ; sử dụng để gộp các project với nhau.

**core** \(required\) Version của Drupal core nơi mà  theme của bạn tương thích vớii. R

**base theme** \(default = Stable\) The machine name of an installed theme to be used as a base theme. If no base theme is set, then the core base theme "Stable" will be used. Classy is the other base theme alternative provided in core. If no base theme should be used, enter "false" as a value for this key. \([Change record](https://www.drupal.org/node/2580687)\)

#### Clear the cache

#### Verify your theme tồn tại hay chưa 

Cuối cùng , vào trang _Appearance_ \(admin/appearance\) . Bạn sẽ thấy Ice Cream theme được list bên dưới mục _Uninstalled themes._

### _C._ Add an Asset Library

### What are asset libraries?

Asset libraries are simply collections of CSS or JavaScript files or settings bundled together under a uniquely identified library name. By bundling files together into asset libraries developers are now able to isolate and package the styling and functionality of a particular component into a reusable library. Once this library has been created adding it to a page, or one particular type of element, is done in the same fashion regardless of the contents of the library. This means there is now one unified mechanism for adding CSS and JavaScript whether it's being added in a module or a theme. Consistency for the win!

### The Classy libraries

We can take a look at some libraries provided by the modules and themes in Drupal 8 core to see examples of this in practice. The Classy theme \(_core/themes/classy_\) provides a handful of libraries we can take a look at. Libraries are specified within a _.libraries.yml_ file.

![Classy theme files](https://drupalize.me/sites/default/files/tutorials/classy-libraries.png)

Here is the contents of the _classy.libraries.yml_ file:

```text
    base:
      version: VERSION
      css:
        component:
          css/components/action-links.css: { weight: -10 }
          css/components/breadcrumb.css: { weight: -10 }
          css/components/button.css: { weight: -10 }
          css/components/collapse-processed.css: { weight: -10 }
          css/components/container-inline.css: { weight: -10 }
          css/components/details.css: { weight: -10 }
          css/components/exposed-filters.css: { weight: -10 }
          css/components/field.css: { weight: -10 }
          css/components/form.css: { weight: -10 }
          css/components/icons.css: { weight: -10 }
          css/components/inline-form.css: { weight: -10 }
          css/components/item-list.css: { weight: -10 }
          css/components/link.css: { weight: -10 }
          css/components/links.css: { weight: -10 }
          css/components/menu.css: { weight: -10 }
          css/components/more-link.css: { weight: -10 }
          css/components/pager.css: { weight: -10 }
          css/components/tabledrag.css: { weight: -10 }
          css/components/tableselect.css: { weight: -10 }
          css/components/tablesort.css: { weight: -10 }
          css/components/tabs.css: { weight: -10 }
          css/components/textarea.css: { weight: -10 }
          css/components/ui-dialog.css: { weight: -10 }

    book-navigation:
      version: VERSION
      css:
        component:
          css/components/book-navigation.css: {}

    dialog:
      version: VERSION
      css:
        component:
          css/components/dialog.css: { weight: -10 }

    dropbutton:
      version: VERSION
      css:
        component:
          css/components/dropbutton.css: { weight: -10 }

    file:
      version: VERSION
      css:
        component:
          css/components/file.css: { weight: -10 }

    forum:
      version: VERSION
      css:
        component:
          css/components/forum.css: { weight: -10 }

    indented:
      version: VERSION
      css:
        component:
          css/components/indented.css: {}

    messages:
      version: VERSION
      css:
        component:
          css/components/messages.css: { weight: -10 }

    node:
      version: VERSION
      css:
        component:
          css/components/node.css: { weight: -10 }

    progress:
      version: VERSION
      css:
        component:
          css/components/progress.css: { weight: -10 }

    search-results:
      version: VERSION
      css:
        component:
          css/components/search-results.css: {}

    user:
      version: VERSION
      css:
        component:
          css/components/user.css: { weight: -10 }

```

We can see here that the Classy theme provides several base CSS components for things like breadcrumbs, buttons, item lists, and pagers \(among others\). All of these asset libraries are composed entirely of CSS files.

### Core libraries

We can see more complex libraries in action in _/core/core.libraries.yml_. This file has an example of a JavaScript library as well as one that provides a dependency on another library.

```text
      # All libraries are defined in alphabetical order.

      backbone:
        remote: https://github.com/jashkenas/backbone
        version: "1.2.3"
        license:
          name: MIT
          url: https://github.com/jashkenas/backbone/blob/1.2.3/LICENSE
          gpl-compatible: true
        js:
          assets/vendor/backbone/backbone-min.js: { weight: -19, minified: true }
        dependencies:
          - core/underscore

```

Here we can see the definition of the Backbone library, including version information, settings indicating it's weight relative to other JavaScript files, and a dependency on the underscore library. The underscore library is defined further down in the _/core/core.libraries.yml_ file.

Take a look at some of the jQuery UI libraries defined by core to see an example of a library that contains both CSS and JavaScript files.

### 





