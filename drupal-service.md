# Drupal Service

Trong Drupal 8, service là bất kì 1 object nào được quản lý bởi 1 services container. Mục đích của service là nhằm tách rời các hàm có thể tái sử dụng bằng cách khởi tạo chúng cùng 1 service container. Cách vận dụng service cung cấp bởi drupal  tốt nhất là truy cập chúng qua 1 service container để đảm bảo bản chất tách rời của chúng. 

### Service Container 

1 ứng dụng có thể gồm nhiều các object: 1 "mailer" object sẽ giúp việc gửi mail trong khi 1 object khác có thể giúp bạn lưu dữ liệu vào DB. Gần như tất cả mọi thứ trong app bạn làm đều được thực hiện bởi 1 trong các object trên.

Trong Symfony, các object này được gọi là services và mỗi service được đặt trong 1 object đặc biệt gọi là service container. Nếu ta đã có 1 service container, ta có thể lấy ra service bằng cách sử dụng id của service đó:

```text
$logger = $container->get('logger');
$entityManager = $container->get('doctrine.orm.entity_manager');
```

#### Cài đặt

Các service trong service container có thể được cấu hình theo 1 vài cách: bằng code \( Module\), file XML, file YAML, vv. Cấu hình của service trong Drupal đa số dựa trên các file YAML. Các service liên quan đến core được đặt trong file services.core.yml. Cấu hình này có thể được mở rộng bởi các module và các class ServiceProvider. Việc tải các cấu hình này được xử lý bởi Kernel.

1 VD trong Drupal 8

```text
services:
  ...
  router_listener:
  class: Symfony\Component\HttpKernel\EventListener\RouterListener
  tags:
    - { name: event_subscriber }
  arguments: ['@router']
  ...
  router:
    class: Symfony\Cmf\Component\Routing\ChainRouter
    calls:
      - [setContext, ['@router.request_context']]
      - [add, ['@router.dynamic']]
  ...
```

Trong đoạn code trên 1 service router\_listener được định nghĩa. Property "arguments" định nghĩa rằng tham số đầu tiên của khởi tạo RouterListener nên là '@router', gắn cho service 1 id là 'router'. Router này cũng được định nghĩa trong cấu hình và có class khác so với class được dùng trong Symfony.

#### Service được gắn Tag

Các nhãn \(Tag\) được dùng để tải các service được "gắn nhãn" nhất định.  

### **Các service của core**

Service của core được định nghĩa trong CoreServiceProvider.php và core.services.yml: vd

```text
  ...
  language_manager:
    class: Drupal\Core\Language\LanguageManager
    arguments: ['@language.default']
  ...
  path.alias_manager:
    class: Drupal\Core\Path\AliasManager
    arguments: ['@path.crud', '@path.alias_whitelist', '@language_manager']
  ...
  string_translation:
    class: Drupal\Core\StringTranslation\TranslationManager
  ...
  breadcrumb:
    class: Drupal\Core\Breadcrumb\BreadcrumbManager
    arguments: ['@module_handler']
  ...

```

Mỗi service có thể phụ thuộc vào nhiều service khác. Trong ví dụ trên, path.alias\_manager phụ thuộc vào service path.crud, path.alias\_whitelist và language\_manager được chỉ định trong arguments.

Định nghĩa 1 dependency cho 1 service bằng cách đặt tiền tố cho tên của service phụ thuộc với kí hiệu @, như @language\_manager. \( Kí hiệu @ là cần thiết để cho Drupal thấy rằng tham số truyền vào là 1 service. Nếu không có kí hiệu này, tham số sẽ chỉ là 1 string bình thường.

Khi 1 đoạn code nào đó gọi đến service path.alias\_manager, service container sẽ đảm bảo rằng service path.crud, path.alias\_whitelist và language\_manager được truyền vào constructor của service path.alias\_manager bằng cách: đầu tiên yêu cầu từng service này và truyền lần lượt vào constructor của service path.alias\_manager.

### Truy cập các service

#### Sử dụng tiêm phụ thuộc \(Dependency Injection\)

Tiêm phụ thuộc là phương pháp nên dùng cho việc truy cập và dùng các service trong drupal 8. Thay cho việc gọi đến global services container, các service sẽ được truyền như 1 tham số vào 1 constructor hay được inject qua các setter method.

#### Sử dụng các hàm toàn cục \(Global Functions\)

Class toàn cục của Drupal cung cấp các phương thức tĩnh nhằm truy cập 1 vài các service thong dụng nhất. VD: Drupal::moduleHandler\(\) sẽ trả về service xử lý module hoặc Drupal::translation\(\) sẽ trả về service dịch chuỗi. Ta có thể dùng Drupal::service\(\) để lấy bất kì 1 service đã được định nghĩa nào.

VD: Truy cập vào service database thông qua \Drupal::database\(\)

```text
// Returns a Drupal\Core\Database\Connection object.
$connection = \Drupal::database();
$result = $connection->select('node', 'n')
  ->fields('n', array('nid'))
  ->execute();

```

VD: Truy cập vào service ngày thông qua phương thức \Drupal::service\(\)

```text
// Returns a Drupal\Core\Datetime\DateFormatter object.
$date = \Drupal::service('date.formatter');

```

#### Tạo custom service

* Bước 1: Tạo file .info.yml \[custom\_services\_example.info.yml\]

```text
name: Custom Services Example
type: module
description: The module provide the sample code to define  your service from  your custom module.
core: 8.x
package: Examples
```

* Bước 2:   Tạo file ‘mymodulename.services.yml’ \[custom\_services\_example.services.yml\]

```text
services:
 custom_services_example.say_hello:
   class: Drupal\custom_services_example\HelloServices
```

‘custom\_services\_example’ là tên module, và ‘custom\_services\_example.say\_hello’ là tên service. Tên class cho service. ‘Drupal\custom\_services\_example\HelloServices’ được đặt trong thư mục src.

* Bước 3:

Tạo class ‘HelloServices.php’ đặt trong thư mục ‘src’

```text
<?php
/**
* @file providing the service that say hello world and hello 'given name'.
*
*/
namespace  Drupal\custom_services_example;
class HelloServices {
 protected $say_something;
 public function __construct() {
   $this->say_something = 'Hello World!';
 }
 public function  sayHello($name = ''){
   if (empty($name)) {
     return $this->say_something;
   }
   else {
     return "Hello " . $name . "!";
   }
 }
}
```

**Cách gọi service đã khởi tạo:**

$service = \Drupal::service\(‘custom\_services\_example.say\_hello’\);

Cách kiểm tra xem service có chạy hay không: bật module devel và đến đường dẫn ‘devel/php’ và chạy đoạn code sau

$service = \Drupal::service\('custom\_services\_example.say\_hello'\);  
 dsm\($service\);  
 dsm\($service-&gt;sayHello\('rakesh'\)\);

Output nếu thành công:

Drupal\custom\_services\_example\HelloServices Object  
 \(     
       \[say\_something:protected\] =&gt; Hello World!     
       \[\_serviceId\] =&gt; custom\_services\_example.say\_hello  
 \)

Hello rakesh!

