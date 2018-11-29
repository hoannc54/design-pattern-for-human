# design-pattern-for-human
![Design Patterns cho mọi người](https://cloud.githubusercontent.com/assets/11269635/23065273/1b7e5938-f515-11e6-8dd3-d0d58de6bb9a.png)

***

<p align="center">
🎉 Giải thích cực kỳ đơn giản cho design patterns! 🎉
</p>
<p align="center">
Một chủ đề có thể dễ dàng làm cho tâm trí của bất cứ ai lay động. Ở đây tôi cố gắng làm cho chúng in sâu vào tâm trí bạn (và có thể là của tôi) bằng cách giải thích chúng theo cách đơn giản nhất có thể.
</p>

***

<sub>Xem qua [blog](http://kamranahmed.info) của tôi và nói "xin chào" trên [Twitter](https://twitter.com/kamranahmedse).</sub>

Giới thiệu
=================

Design pattern là những giải pháp cho những vấn đề thường gặp; **hướng dẫn cách giải quyết cho những vấn đề nhất định**. Chúng không phải là những class, package hay thư viện mà bạn có thể nhúng vào ứng dụng của bạn và chờ đợi điều kì diệu xảy ra. Mà chúng chỉ là những hướng dẫn về cách giải quyết các vấn đề nhất định trong những tình huống nhất định.

> Design pattern là những giải pháp cho những vấn đề thường gặp; hướng dẫn giải quyết các vấn đề nhất định.

Wikipedia mô tả chúng như sau:

> Trong lĩnh vực kĩ thuật phần mềm, một design pattern của phần mềm là một giải pháp cho việc tái sử dụng chung cho những vấn đề thường xảy ra trong lĩnh vực thiết kế phần mềm. Nó không phải là những thiết kế hoàn chỉnh có thể chuyển thành mã nguồn hoặc mã máy. Nó chỉ là mô tả hoặc template cho việc làm sao để giải quyết vấn đề có thể sử dụng cho các tình huống khác nhau.

⚠️ Hãy cẩn thận
-----------------
- Các design pattern không phải là những viên đạn bạc cho tất cả các vấn đề của bạn.
- Đừng cố ép buộc chúng; những thứ rất tệ có thể sẽ xảy ra nếu làm như vậy.
- Nhớ những design pattern này chỉ là giải pháp cho các vấn đề, không phải là giải pháp để tìm ra các vấn đề; vì thế nên đừng nghĩ quá nhiều về nó.
- Nếu sử dụng đúng lúc đúng chỗ, chúng có thể chứng minh mình là những vị cứu tinh, hoặc chúng có thể dẫn tới một mớ code hỗn độn kinh khủng.

> Chú ý thêm là các ví dụ code thực hiện trên PHP-7, tuy nhiên điều này không ảnh hưởng tới bạn vì các khái niệm là giống nhau.

Các loại Design Pattern
-----------------

* [Creational](#creational-design-patterns)
* [Structural](#structural-design-patterns)
* [Behavioral](#behavioral-design-patterns)

Creational Design Patterns
==========================

Nói một cách đơn giản
> Các creational pattern tập trung vào việc làm sao để khởi tạo một đối tượng hoặc một nhóm các đối tượng có liên hệ với nhau.

Wikipedia định nghĩa như sau:
> Trong lĩnh vực kĩ thuật phần mềm, các creational design pattern là những design pattern sử dụng cho việc khởi tạo các đối tượng, cố gắng tạo các đối tượng theo cách phù hợp nhất với mỗi tình huống khác nhau. Hình thức tạo một đối tượng cơ bản có thể dẫn đến các vấn đề về thiết kế hoặc làm tăng độ phức tạp của thiết kế. Các creational design pattern giải quyết vấn đề bằng cách kiểm soát việc tạo đối tượng này.
 * [Simple Factory](#-simple-factory)
 * [Factory Method](#-factory-method)
 * [Abstract Factory](#-abstract-factory)
 * [Builder](#-builder)
 * [Prototype](#-prototype)
 * [Singleton](#-singleton)

🏠 Simple Factory
--------------
Ví dụ thực tế
> Hãy xem xét, bạn đang xây dựng một ngôi nhà và bạn cần cửa ra vào. Bạn có thể mặc quần áo thợ mộc, mang một ít gỗ, keo, đinh và tất cả các dụng cụ cần thiết để làm cửa và bắt đầu làm nó trong nhà hoặc bạn chỉ cần gọi nhà máy và nhận cửa được làm cho bạn để bạn không cần phải tìm hiểu bất cứ điều gì về việc làm cửa hoặc để đối phó với mớ hỗn độn mà đi kèm với làm cho nó..

Nói một cách đơn giản
> Simple factory chỉ đơn giản là tạo ra những phiên bản cho client mà không cần lộ ra bất kì một logic về việc khởi tạo nào tới phía người dùng.

Wikipedia nói rằng
> Trong lập trình hướng đối tượng (OOP), một factory là một object được dùng để tạo ra các object khác - thường thì factory là một function hoặc method trả về những object nguyên bản hoặc class từ những method được gọi, được coi giống như là "new".

**ví dụ về lập trình**

Đầu tiên chúng ta có một interface của cửa và implementation.

```php
interface Door
{
    public function getWidth(): float;
    public function getHeight(): float;
}

class WoodenDoor implements Door
{
    protected $width;
    protected $height;

    public function __construct(float $width, float $height)
    {
        $this->width = $width;
        $this->height = $height;
    }

    public function getWidth(): float
    {
        return $this->width;
    }

    public function getHeight(): float
    {
        return $this->height;
    }
}
```

Tiếp theo chúng ta có factory tạo ra cửa và trả về nó

```php
class DoorFactory
{
    public static function makeDoor($width, $height): Door
    {
        return new WoodenDoor($width, $height);
    }
}
```

Và nó có thể sử dụng như sau

```php
// tạo một cái cửa có kích thước 100x200
$door = DoorFactory::makeDoor(100, 200);

echo 'Width: ' . $door->getWidth();
echo 'Height: ' . $door->getHeight();

// tạo một cái cửa có kích thước 50x100
$door2 = DoorFactory::makeDoor(50, 100);
```

**Sử dụng khi nào?**

Khi tạo một đối tượng không chỉ là một vài nhiệm vụ và liên quan đến một số logic, nó có ý nghĩa để đặt nó trong một factory chuyên dụng thay vì lặp lại cùng một code ở khắp mọi nơi.

🏭 Factory method
--------------

Ví dụ thực tế

> Xem xét trường hợp của một người quản lý về tuyển dụng. Một người không thể phỏng vấn ở mỗi vị trí. Dựa trên những công việc đang mở, cô ấy phải quyết định và ủy nhiệm các bước phỏng vấn cho những người khác nhau..

Nói một cách đơn giản
> Nó cung cấp một cách để ủy quyền logic instantiation cho các lớp con. 

Wikipedia định nghĩa là 
> Trong lập trình dựa trên lớp, factory method pattern là một creational pattern mà sử dụng các method factory để giải quyết vấn đề về khởi tạo các object mà không cần xác định chính xác class của object mà sẽ được tạo ra. Điều này được thực hiện bằng cách tạo ra những object thông qua việc gọi một method factory - hoặc được chỉ định trong interface và implement bởi các class con, hoặc được implement trong class base và ghi đè tùy ý bởi các class dẫn xuất - thay vì được gọi thông qua hàm khởi tạo.

 **Ví dụ trong lập trình**

lấy ví dụ về quản lý tuyển dụng ở trên. Đầu tiên chúng ta có một interface interviewer và một vài class implement nó.

```php
interface Interviewer
{
    public function askQuestions();
}

class Developer implements Interviewer
{
    public function askQuestions()
    {
        echo 'Asking about design patterns!';
    }
}

class CommunityExecutive implements Interviewer
{
    public function askQuestions()
    {
        echo 'Asking about community building';
    }
}
```

Bây giờ chúng ta tạo ra `HiringManager`

```php
abstract class HiringManager
{

    // Factory method
    abstract protected function makeInterviewer(): Interviewer;

    public function takeInterview()
    {
        $interviewer = $this->makeInterviewer();
        $interviewer->askQuestions();
    }
}

```

Giờ mọi child có thể extend nó và được cung cấp cho các interviewer một cách bắt buộc

```php
class DevelopmentManager extends HiringManager
{
    protected function makeInterviewer(): Interviewer
    {
        return new Developer();
    }
}

class MarketingManager extends HiringManager
{
    protected function makeInterviewer(): Interviewer
    {
        return new CommunityExecutive();
    }
}
```

và sau đó nó có thể sử dụng như sau

```php
$devManager = new DevelopmentManager();
$devManager->takeInterview(); // Output: Asking about design patterns

$marketingManager = new MarketingManager();
$marketingManager->takeInterview(); // Output: Asking about community building.
```

**Sử dụng khi nào?**

Nó hữu dụng khi có một số việc được sử lý chung trong một class nhưng các class con được yêu cầu có thể được đưa ra bởi các quyết định linh động trong khi chạy. Hay nói cách khác, khi client không biết chính xác class con nào là cần thiết.

🔨 Abstract Factory
----------------

Ví dụ thực tế
>Mở rộng ví dụ cửa của chúng tôi từ Simple Factory. Căn cứ vào nhu cầu của bạn, bạn có thể nhận được một cánh cửa gỗ từ một cửa gỗ, cửa sắt từ một cửa hàng sắt hoặc cửa nhựa PVC từ cửa hàng liên quan. Thêm vào đó bạn có thể cần một chàng trai với các kỹ năng khác nhau để phù hợp với cánh cửa, ví dụ như thợ mộc cho cửa gỗ, thợ hàn cho cửa sắt vv Như bạn thấy có sự phụ thuộc giữa cửa ra vào, cửa gỗ cần thợ mộc, cửa sắt cần thợ hàn, v.v.

Nói một cách ngắn gọn
> một factory của các factory; một factory nhóm những cá thể nhưng các factory liên kết/phụ thuộc lẫn nhau mà không cần chỉ rõ các class cụ thể của nó.

Wikipedia định nghĩa là 
> abstract factory pattern cung cấp một cách để đóng gói một nhóm những cá thể factory có cùng một chủ đề mà không cần khai báo class cụ thể của chúng.

**Ví dụ trong lập trình**

Sử dụng lại ví dụ về cửa ở trên. Đầu tiên chúng ta có một interface `Door` và một vài class khác implement nó

```php
interface Door
{
    public function getDescription();
}

class WoodenDoor implements Door
{
    public function getDescription()
    {
        echo 'I am a wooden door';
    }
}

class IronDoor implements Door
{
    public function getDescription()
    {
        echo 'I am an iron door';
    }
}
```

Sau đó chúng ta sử dụng một vài chuyên gia phù hợp với mỗi loại cửa

```php
interface DoorFittingExpert
{
    public function getDescription();
}

class Welder implements DoorFittingExpert
{
    public function getDescription()
    {
        echo 'I can only fit iron doors';
    }
}

class Carpenter implements DoorFittingExpert
{
    public function getDescription()
    {
        echo 'I can only fit wooden doors';
    }
}
```

Bây giờ chúng ta có abstract factory sẽ cho phép chúng ta tạo ra một nhóm các object có liên quan tới nhau. ví dụ như nhà máy cửa gỗ sẽ tạo ra cửa gỗ và chuyên gia phù hợp với cửa gỗ, và nhà máy cửa sắt tạo ta cửa sắt và chuyên gia phù hợp với cửa sắt.

```php
interface DoorFactory
{
    public function makeDoor(): Door;
    public function makeFittingExpert(): DoorFittingExpert;
}

// Wooden factory to return carpenter and wooden door
class WoodenDoorFactory implements DoorFactory
{
    public function makeDoor(): Door
    {
        return new WoodenDoor();
    }

    public function makeFittingExpert(): DoorFittingExpert
    {
        return new Carpenter();
    }
}

// Iron door factory to get iron door and the relevant fitting expert
class IronDoorFactory implements DoorFactory
{
    public function makeDoor(): Door
    {
        return new IronDoor();
    }

    public function makeFittingExpert(): DoorFittingExpert
    {
        return new Welder();
    }
}
```

Và sau đó nó có thể được sử dụng như sau:

```php
$woodenFactory = new WoodenDoorFactory();

$door = $woodenFactory->makeDoor();
$expert = $woodenFactory->makeFittingExpert();

$door->getDescription();  // Output: I am a wooden door
$expert->getDescription(); // Output: I can only fit wooden doors

// Same for Iron Factory
$ironFactory = new IronDoorFactory();

$door = $ironFactory->makeDoor();
$expert = $ironFactory->makeFittingExpert();

$door->getDescription();  // Output: I am an iron door
$expert->getDescription(); // Output: I can only fit iron doors
```

Như bạn có thể thấy thì một nhà máy cửa gỗ được đóng gói cả `thợ mộc` và `cửa gỗ` cũng như nhà máy cửa sắp đóng gói cả `cửa sắt` và `thợ hàn`. Và do đó nó đảm bảo với chúng tôi là với mỗi cánh cửa được tạo ra, chúng tôi sẽ không lấy nhầm một chuyên gia.

**Sử dụng khi nào?**

Khi có sự tương quan giữa phụ thuộc và các logic khởi tạo liên quan không đơn giản

👷 Builder
--------------------------------------------
Ví dụ thực tế

> Hãy tưởng tượng là bạn đang ở Hardee's và bạn đặt một đơn hàng đặc biệt, hãy nói "Big hardee" và họ đưa cho bạn mà không có *bất kì câu hỏi nào*; đây là một ví dụ về simple factory.  Nhưng đâu là những trường hợp khi logic khởi tạo liên quan tới nhiều bước. Ví dụ như bạn muốn tùy chỉnh đơn Subway,bạn có một số tùy chọn về cách thức làm bánh burger của bạn, ví dụ: bạn muốn bánh mì nào? loại sốt mà bạn muốn?Bạn muốn phô mai nào?... Trong những trường hợp như vậy, builder pattern được sử dụng như một giải pháp.

Nói một cách ngắn gọn
> Cho phép bạn tạo các đặc điểm khác nhau của object trong khi tránh bị ảnh hưởng việc khởi tạo. Nó hữu dụng khi có thể tạo nhiều tùy chọn cho một object. Hoặc khi có quá nhiều bước trong việc tạo ra một object.

Wikipedia định nghĩa là
> Builder pattern là một object thuộc nhóm design pattern khởi tạo phần mềm với ý tưởng tìm kiếm giải pháp constructor anti-pattern.

Hãy để tôi giới thiệu thêm một chút về mô hình chống lại việc khởi tạo này. Tại một thời điểm khác, chúng tôi đã thấy một constructor như dưới đây:

```php
public function __construct($size, $cheese = true, $pepperoni = true, $tomato = false, $lettuce = true)
{
}
```

Như bạn thấy, số lượng tham số của hàm khởi tạo có thể nhanh chóng mất kiểm soát và nó dần trở nên rất khó hiểu về sự sắp xếp các tham số. Thêm nữa là danh sách những tham số có thể tiếp tục phát triển nếu bạn muốn thêm nhiều option trong tương lai. Điều này được gọi là mô hình constructor anti-pattern.

**Ví dụ trong lập trình**

Cách thay thế hợp lý là sử dụng builder pattern. Đầu tiên chúng ta đang muốn làm một chiếc bánh mì kẹp cho mình.

```php
class Burger
{
    protected $size;

    protected $cheese = false;
    protected $pepperoni = false;
    protected $lettuce = false;
    protected $tomato = false;

    public function __construct(BurgerBuilder $builder)
    {
        $this->size = $builder->size;
        $this->cheese = $builder->cheese;
        $this->pepperoni = $builder->pepperoni;
        $this->lettuce = $builder->lettuce;
        $this->tomato = $builder->tomato;
    }
}
```

Và chúng ta có một builder

```php
class BurgerBuilder
{
    public $size;

    public $cheese = false;
    public $pepperoni = false;
    public $lettuce = false;
    public $tomato = false;

    public function __construct(int $size)
    {
        $this->size = $size;
    }

    public function addPepperoni()
    {
        $this->pepperoni = true;
        return $this;
    }

    public function addLettuce()
    {
        $this->lettuce = true;
        return $this;
    }

    public function addCheese()
    {
        $this->cheese = true;
        return $this;
    }

    public function addTomato()
    {
        $this->tomato = true;
        return $this;
    }

    public function build(): Burger
    {
        return new Burger($this);
    }
}
```

Và sau đó có thể sử dụng như sau:

```php
$burger = (new BurgerBuilder(14))
                    ->addPepperoni()
                    ->addLettuce()
                    ->addTomato()
                    ->build();
```

**Sử dụng khi nào?**

Khi có thể có một số đặc điểm của object và tránh việc chống lại khởi tạo. Sự khác biệt chính của factory pattern là đây; factory pattern được sử dụng khi việc khởi tạo chỉ tạo ra một bước trong tiến trình trong khi builder pattern được sử dụng khi có nhiều bước trong quá trình.

🐑 Prototype
------------
Ví dụ thực tế
> Bạn có nhớ dolly? Con cừu mà được nhân bản! Việc cho phép không nhận những thông tin chi tiết nhưng điểm mấu chốt ở đây là tất cả những thứ được nhân bản.

Nói một cách ngắn gọn
> Việc tạo object dựa trên một object đã tồn tại thông qua việc nhân bản.

Wikipedia định nghĩa là:
> Prototype pattern là một creational design pattern trong phát triển phần mềm. Nó được sử dụng khi kiểu của object cần tạo được định nghĩa bởi một thực thể nguyên mẫu, giống như việc nhân bản nó để tạo ra một object mới.

Nói ngắn gọn, nó cho phép bạn tạo một bản sao một object đã tồn tại và sửa đổi nó theo nhu cầu của bạn thay vì trải qua các sự cố khi tạo một object từ đầu và thiết lập lại nó.

**Ví dụ trong lập trình**

Trong PHP, nó khá dễ dàng để sử dụng `clone`

```php
class Sheep
{
    protected $name;
    protected $category;

    public function __construct(string $name, string $category = 'Mountain Sheep')
    {
        $this->name = $name;
        $this->category = $category;
    }

    public function setName(string $name)
    {
        $this->name = $name;
    }

    public function getName()
    {
        return $this->name;
    }

    public function setCategory(string $category)
    {
        $this->category = $category;
    }

    public function getCategory()
    {
        return $this->category;
    }
}
```

Sau đó nó có thể clone như dưới đây

```php
$original = new Sheep('Jolly');
echo $original->getName(); // Jolly
echo $original->getCategory(); // Mountain Sheep

// Clone and modify what is required
$cloned = clone $original;
$cloned->setName('Dolly');
echo $cloned->getName(); // Dolly
echo $cloned->getCategory(); // Mountain sheep
```

bạn cũng có thể sử dụng magic method `__clone` để sửa đổi các hành vi khi nhân bản.

**sử dụng khi nào?**

Khi một object được yêu cầu phải tương tự như object hiện có hoặc khi việc khởi tạo mất nhiều công hơn việc nhân bản.

💍 Singleton
------------

Ví dụ thực tế
> Cùng một lúc chỉ có thể có một tổng thống đối với mỗi quốc gia. Cùng một tổng thống phải đưa ra được hành động. Tổng thống ở đây là một singleton.

Nói một cách ngắn gọn 
> Đảm bảo là chỉ có một đối tượng duy nhất của mỗi class được tạo ra.

Wikipedia định nghĩa là
>Trong kĩ thuật phần mềm,singleton patternn là một mẫu thiết kế phần mềm hạn chế sự khởi tạo của một lớp thành một đối tượng. Điều này rất hữu ích khi cần một đối tượng chính xác để điều phối các hành động trên toàn hệ thống..

Singleton pattern thực sự được coi là một mô hình anti-pattern và nên tránh lạm dụng nó . Nó không nhất thiết là xấu và có thể có một số trường hợp sử dụng hợp lệ nhưng nên được sử dụng thận trọng vì nó đưa ra một trạng thái toàn cục trong ứng dụng của bạn và thay đổi nó ở một nơi có thể ảnh hưởng đến các khu vực khác và nó có thể trở nên khá khó khăn để gỡ lỗi. Điều tệ hại khác về họ là nó làm cho mã của bạn được kết hợp chặt chẽ cộng với việc singleton có thể khó khăn..

**Ví dụ về lập trình**

Để tạo ra một singleton, làm cho hàm tạo riêng, vô hiệu hóa nhân bản, vô hiệu hóa phần mở rộng và tạo một biến tĩnh để chứa cá thể đó
```php
final class President
{
    private static $instance;

    private function __construct()
    {
        // Hide the constructor
    }

    public static function getInstance(): President
    {
        if (!self::$instance) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    private function __clone()
    {
        // Disable cloning
    }

    private function __wakeup()
    {
        // Disable unserialize
    }
}
```
Sau đó, để sử dụng
```php
$president1 = President::getInstance();
$president2 = President::getInstance();

var_dump($president1 === $president2); // true
```

