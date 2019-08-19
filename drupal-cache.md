---
description: Cache API
---

# DRUPAL CACHE

## Cache API: 

### Định nghĩa: 

1 cache là 1 thành phần thuộc phần cứng hay phần mềm có chứa dữ liệu, nhằm mục đích tăng tốc độ xử lý dữ liệu đó khi nó được gọi tới. Dữ liệu trong 1 cache có thể là kết quả của việc tính toán trước đó, hoặc là 1 bản sao dữ liệu được lưu ở đâu đó.

### Cache hit, cache miss:

Cache hit: xảy ra khi dữ liệu được gọi có thể được tìm thấy trong cache, trong khi ngược lại thì gọi là cache miss. Dữ liệu khi cache hit sẽ được lấy ra từ cache, điều này nhanh hơn việc tính toán kết quả 1 lần nữa hoặc lấy dữ liệu ra từ nơi khác. Vì thế, càng nhiều dữ liệu được gọi ra từ cache, thì hệ thống càng xử lý nhanh hơn. Cache API trong drupal 8 chứa các dữ liệu mất thời gian để tính toán.

### Xử lý dữ liệu cache:

Cách dữ liệu được lưu trữ vào các backend và bin:

* Khi xử lý 1 request HTTP, thông tin được lưu trong các bin khác nhau, mỗi bin này được lưu trữ trong các backend.
* Backend là 1 cơ chế lưu trữ: database SQL, Memcache, thậm chí là các file trong ổ đĩa.
* Khi request 1 cache object, có thể tùy chỉnh tên của bin khi gọi đến \Drupal::cache\(\).

Hoặc, có thể request 1 bin bằng việc get service “cache.nameofbin” từ container. Bin mặc định được đặt là “default”, với tên service là “cache.default”, dùng để lưu trữ các dữ cache hay được sử dụng.

1 module có thể tự định nghĩa cache bin cho riêng nó trong file modulename.services.yml như sau\]

```text
cache.nameofbin:
 class: Drupal\Core\Cache\CacheBackendInterface
 tags:
   - { name: cache.bin }
 factory: cache_factory:get
 arguments: [nameofbin]
```

Một vài cache bin hay dùng: bootstrap, render,data, discovery

### Bin

Được map đến các bảng trong db có tiền tố cache\_ . Khi tương tác với cache, ta luôn bắt đầu bằng việc request 1 bin:

```text
$cache = \Drupal::cache();
```

$cache là instance của 1 object DatabaseBackend đại diện cho bin mặc định \( cache\_default\). Để yêu cầu 1 bin cụ thế, ta truyền tên bin vào constructor:

```text
$render_cache = \Drupal::cache('render');
```

Lấy ra các cache:

```text
$cache = \Drupal::cache()->get('my_value');
```

$cache là 1 object stdClass chứa metadata + với dữ liệu thật trong $cache-&gt;data. Tham số my\_value là cache ID

Lưu lại 1 cache:

Sử dụng method set\(\), method này cần 2 tham số bắt buộc và 2 tham số lựa chọn:

* Cache ID
* Dữ liệu \(có thể là 1 chuỗi, mảng\)
* Thời gian tồn tại cache
* Tag

Ví dụ:

```text
Drupal::cache()->set('my_value', $my_object, CacheBackendInterface::CACHE_PERMANENT, array('my_first_tag', 'my_second_tag'));
```

**Xóa và vô hiệu hóa cache**‌

Cache có thể bị xóa bằng việc dùng method garbageCollection\(\). Khi 1 chace hết hạn tồn tại, cache này bị coi là vô hiệu nhưng vẫn tồn tại trong bin và có thể được lấy ra. Ta có thể vô hiệu chúng bằng các method invalidate\(\), invalidateMultiple\(\) hoặc invalidateAll\(\). Có thể xóa bằng method delete\(\), deleteMultiple hoặc deleteAll\(\) , điều này sẽ xóa các bản ghi liên quan đến cache bị xóa trong db‌

### Cache Properties <a id="cache-properties"></a>

‌

1 cache có 3 properties là context, tags, max-age.

```text
'#cache' => [    'contexts' => ['languages', 'timezone'],    'tags' => ['node:5', 'user:3'],    'max-age' => Cache::PERMANENT,    ],
```

‌

#### Tag <a id="tag"></a>

‌

 Dùng để nhận dạng các cache items trong nhiều bin khác nhau. Mục đích của tag là để chỉ định 1 cách chính xác các cache item giống data với nhau.‌

#### Context <a id="context"></a>

‌

 Cache context là cái gì đó cho phép bộ nhớ đệm của sự thay đổi khác nhau của một cái gì đó \(ví dụ nội dung hoặc kết quả của một số phức tạp, thời gian dài / tài nguyên tính toán\). Cache context tương tự như [HTTP-Vary](https://www.w3.org/Protocols/HTTP/Issues/vary-header.html)\(các thay đổi của bộ nhớ cache\). Theo định nghĩa [D.O](http://www.drupal.org/).

> > “Cache contexts provide a declarative way to create context-dependent variations of something that needs to be cached.”

‌

Những gì tôi phát hiện ra trong quá trình tra cứu cache context là một điều tổng quát. Bởi vì tổng quát có nghĩa là bất kỳ thông tin có sẵn hoặc có thể nhận được trên mọi yêu cầu như thông tin người dùng, IP, session, vv . Nếu cái gì đó không phải là toàn cầu hoặc không thể xác định trong mỗi yêu cầu, chúng tôi không thể sử dụng nó cho bối cảnh bộ nhớ cache \(một lần nữa AFAIK\) . Một ví dụ là thông tin nút hoặc thông tin trường nút. Chúng ta không thể có / lấy thông tin về một nút trên mọi yêu cầu và do đó không thể sử dụng nó như là bối cảnh bộ nhớ cache \(một lần nữa AFAIK\), mặt khác chúng ta hãy lấy ví dụ về người dùng. Chúng tôi có thông tin người dùng có sẵn trên toàn cầu \(cho mỗi yêu cầu\) và do đó chúng tôi có thể sử dụng nó trong cache context. Tương tự phiên, cookie, IP là một cái gì đó mà chúng tôi có trên mọi yêu cầu và do đó có thể được sử dụng cho cache context.‌

Hãy thảo luận về trường hợp sử dụng cache context. Một khách hàng muốn hiển thị vai trò của người dùng hiện tại trong một khối. Để đơn giản, chúng tôi giả định rằng một vai trò có thể được gán cho người dùng \(ngoại trừ vai trò được chứng thực\). Trong Drupal 7, điều này có thể được thực hiện dễ dàng. Nhưng khách hàng cũng muốn bộ nhớ đệm đúng . Đây là điều khó khắn. Trong Drupal 7, chúng tôi có cấp độ trang và bộ nhớ đệm cấp khối. Bộ nhớ đệm cấp trang chỉ hoạt động cho người dùng ẩn danh, do đó, bộ nhớ đệm cấp độ chặn là lựa chọn duy nhất của chúng tôi, nhưng vấn đề với bộ nhớ đệm cấp độ khối là nó không cung cấp biến thể. Nó sẽ cache khối cho lần truy cập đầu tiên của người dùng và hiển thị cùng một dữ liệu với người khác \(không quan tâm nếu người dùng có vai trò khác nhau\).‌

Drupal 8 có giải pháp trong xây dựng cho các vấn đề trên \(cache ngữ cảnh \). Drupal 8 lõi cung cấp bối cảnh bộ nhớ cache user.roles cho phép thay đổi bộ nhớ cache dựa trên vai trò người dùng. Vì vậy, nếu người dùng có vai trò 'A' xuất hiện lần đầu tiên, khối sẽ được lưu trữ. Lần thứ hai nếu cùng / người dùng khác nhau có vai trò 'A' đến, phiên bản đã lưu trong bộ nhớ cache sẽ được phục vụ. Nếu người dùng khác có vai trò 'B' xuất hiện, thì phiên bản được lưu trữ trong bộ nhớ cache sẽ được phục vụ. Lần thứ hai đối với người dùng có vai trò 'B', phiên bản đã lưu trong bộ nhớ cache sẽ được sử dụng.

#### Max-age

Tính bằng giây, max-age kiểm soát thời gian tồn tại của 1 cache.

#### Xóa cache trên drupal

Có 3 cách:

* Dùng giao diện admin: vào URL _admin/config/development/performance, chọn clear all cache_
* Dùng script rebuild: mở file setting.php, thêm đoạn code này vào cuối file:

```text
$settings['rebuild_access'] = TRUE;
```

Sau đó truy cập vào /core/rebuild.php

* Dùng console: drush cache-rebuild

#### Các module hỗ trợ cache:

* Internal Page Cache: Cache các trang web cho người dùng ẩn danh, cải thiện đáng kể performance của trang. Tuy nhiên module này cần được vô hiệu hóa trên các website cung cấp 1 vài  nội dung  cá nhân cho người dùng ẩn danh.
* Dynamic Page Cache: Chức năng giống module trên nhưng có thêm các cải tiến. Cache của module này không chỉ hoạt động với user  ẩn danh mà còn với user đã log in. Trang web sẽ được cache trừ các content cá nhân của nó.

#### 1 vài câu lệnh setting về cache:

```text
-	<?php
-	 
-	// Set an expiring cache item
-	\Drupal::cache()-&gt;set('cache_key', 'cache_data', $expiration_timestamp);
-	 
-	// Set a permanent cache item
-	\Drupal::cache()-&gt;set('cache_key', 'cache_data', CacheBackendInterface::CACHE_PERMANENT);
-	 
-	// Set a permanent cache item with tags.
-	\Drupal::cache()-&gt;set('cache_key', 'cache_data', CacheBackendInterface::CACHE_PERMANENT, array('tag_one', 'second_tag'));
-	 
-	// Fetch an item from the cache
-	$cache = \Drupal::cache()-&gt;get('cache_key');
-	if (!empty($cache-&gt;data) {
-	  // Do something with $cache-&gt;data here.
-	}
-	 
-	// Invalidate a cache item
-	\Drupal::cache()-&gt;invalidate('cache_key');
-	 
-	// Invalidate multiple cache items
-	\Drupal::cache()-&gt;invalidateMultiple($array_of_cache_ids);
-	 
-	// Invalidate specific cache tags
-	use Drupal\Core\Cache\Cache;
-	 
-	Cache::invalidateTags(['config:block.block.YOURBLOCKID', 
-	  'config:YOURMODULE.YOURCONFIG', 'node:YOURNID']);
-	 
-	// Note that the invalidation functions also exist for deleting caches,
-	// by just replacing invalidate with delete.
-	 
-	// Flush the entire site cache.
-	drupal_flush_all_caches();

```

​

