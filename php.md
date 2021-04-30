### PHP
---

#### MyISAM 和 InnoDB 的基本区别？  
* MyISAM类型不支持事务，表锁，易产生碎片，要经常优化，读写速度较快；
* InnoDB类型支持事务，行锁，有崩溃恢复能力。读写速度比MyISAM慢。

#### 为什么InnoDB比MyISAM速度慢？
* 在查询的时候一般InnoDB是比MyISAM要慢.
  * 因为MyISAM是将索引和数据分开存储的，查询更快；
  * MyISAM不需要维护事务的机制，保持MVCC一致；
  * 数据块缓存，InnoDB缓存数据块，但是MyISAM只缓存索引。  
* 但是MyISAM也有致命缺陷，它使用表锁，使得在并发高的时候，效率更低。它的恢复机制差，在数据库崩溃的时候，难以恢复。它不支持事务。

#### isset() 和 empty() 区别？
* Isset判断变量是否存在，可以传入多个变量，若其中一个变量不存在则返回假。
* empty判断变量是否为空为假，只可传一个变量，如果为空为假则返回真。

####  常用的排序算法？
* 冒泡排序法 O(n*n)
* 快速排序法 不稳定算法，最坏O(n*n), 最好O(nlogn)
* 简单选择排序法 O(n*n)
* 堆排序法、O(nlogn) 分为堆调整O(3n)和堆排序O(nlogn)两部分。参考 ：https://chihminh.github.io/2016/08/08/heap-sort/
* 直接插入排序法 O(n*n)
* 希尔排序法 直接插入排序算法的改进，它对已经有一定顺序的序列比较好用，其 最坏情况时间复杂度为$O(n^2)$,最好为为O(n),平均为$O(n^1.3)$. 可参考： https://my.oschina.net/u/4267438/blog/3302670  
* 归并排序法(Merge sort)。 也是DTU算法课推荐的排序算法，时间复杂度O(nlogn)，空间复杂度O(n).


#### 引用传递在php如何使用？
```
<?php
function foo(&$var)
{
    $var++;
}

$a=5;
foo($a);
// $a is 6 here
?>
```

#### 单例模式，
```
/**
 * 单例类
 * Singleton.class
 */
class Singleton  
{  
   // 静态成品变量 保存全局实例
    private static $_instance = NULL;
    
     // 私有化默认构造方法，保证外界无法直接实例化
       private function __construct() 
       {
       }
       
    // 静态工厂方法，返还此类的唯一实例
     public static function getInstance() {
      if (is_null(self::$_instance)) {
       self::$_instance = new Singleton();
      }
     
      return self::$_instance;
     }
     
   // 防止用户克隆实例
     public function __clone(){
      die('Clone is not allowed.' . E_USER_ERROR);
     }
     
  // 测试   
   public function test()
   {
      echo 'Singleton Test OK!';
   }
     
}  

// 客户端
class Client {
 public static function main() {
  $instance = Singleton::getInstance();
  $instance->test();
 }
}
Client::main();
```
思路还是非常奇妙的，首先一个类的静态方法方便获取单例，在该方法中判断，静态的单例是否存在，如果不存在，实例化类，如果存在，直接返回。

#### UTF8知识 
* 一个utf8数字占1个字节
* 一个utf8英文字母占1个字节
* 少数是汉字每个占用3个字节，多数占用4个字节
* 例子：
```
<?php
$str = " hello你好世界";
echo strlen($str); // 18
?>
```

#### PHP数组相关函数
* array()----创建数组
* array_combine()----通过合并两个数组来创建一个新数组
* range()----创建并返回一个包含指定范围的元素的数组
* compact()----建立一个数组
* array_chunk()----将一个数组分割成多个
* array_merge()----把两个或多个数组合并成一个数组
* array_slice()----在数组中根据条件取出一段值
* array_diff()----返回两个数组的差集数组
* array_intersect()----计算数组的交集
* array_search()----在数组中搜索给定的值
* array_splice()----移除数组的一部分且替代它
* array_key_exists()----判断某个数组中是否存在指定的key
* shuffle()----把数组中的元素按随机顺序重新排列
* array_flip()----交换数组中的键和值
* array_reverse()----将原数组中的元素顺序翻转，创建新的数组并返回
* array_unique()----移除数组中重复的值


#### 接口与抽象类的区别
* 相同点
  * 都不能被实例化 
  * 接口的实现类或抽象类的子类都只有实现了接口或抽象类中的方法后才能实例化。

* 不同点
  * 接口只有定义，不能有方法的实现，抽象类可以有定义与实现，方法可在抽象类中实现。
  * 实现接口的关键字为implements，继承抽象类的关键字为extends。一个类可以实现多个接口，但一个类只能继承一个抽象类。所以，使用接口可以间接地实现多重继承。
  * 接口强调特定功能的实现，而抽象类强调所属关系。

#### mysql_fetch_row() 和mysql_fetch_array之间有什么区别?  
Mysql_fetch_row()是从结果集中取出一行作为枚举数组，mysql_fetch_array()是从结果集中取出一行作为索引数组或关联数组或两种方式都有。

#### 有一个网页地址, 比如PHP开发资源网主页: http://www.phpres.com/index.html,如何得到它的内容?
* file_get_contents
* curl
* socket

#### 写几个魔术方法并说明作用？

* __call()当调用不存在的方法时会自动调用的方法

* __autoload()在实例化一个尚未被定义的类是会自动调用次方法来加载类文件

* __set()当给未定义的变量赋值时会自动调用的方法

* __get()当获取未定义变量的值时会自动调用的方法

* __construct()构造方法，实例化类时自动调用的方法

* __destroy()销毁对象时自动调用的方法

* __unset()当对一个未定义变量调用unset()时自动调用的方法

* __isset()当对一个未定义变量调用isset()方法时自动调用的方法

* __clone()克隆一个对象

* __tostring()当输出一个对象时自动调用的方法


