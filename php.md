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
