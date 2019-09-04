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

