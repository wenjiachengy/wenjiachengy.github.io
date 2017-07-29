---
layout: post
title:  '归并排序'
date:   2017-07-28 23:23:40 +0800
categories: acm
---

#### 思想：先使每个子序列有序，再使子序列段间有序

#### 概念过程：
  - 比较a[i]和b[j]的大小，若a[i]≤b[j]，则将第一个有序表中的元素a[i]复制到r[k]中，并令i和k分别加上1；否则将第二个有序表中的元素b[j]复制到r[k]中，并令j和k分别加上1，如此循环下去，直到其中一个有序表取完，然后再将另一个有序表中剩余的元素复制到r中从下标k到下标t的单元。
  - 归并排序的算法我们通常用递归实现，先把待排序区间[s,t]以中点二分，接着把左边子区间排序，再把右边子区间排序，最后把左区间和右区间用一次归并操作合并成有序的区间[s,t]。

#### 举例过程：
 - 设有数组[6，202，100，301，38，8，1]
 - 取其中间个数7/2=3，那么前3个为一组[6, 202, 100]，剩下4个为一组[301，38，8，1]
 - 同理继续分组把[6, 202, 100]分成[6]和[202, 100]，再把[202, 100]分成[202]和[100]
 - 此时[202]和[100]都是单元素，进行排序，合并成[100, 202]有序数组
 - 此时[6]与[100, 202]进行排序，排序方式很简单，两个数组的元素逐一比较：假设定义a=[6]，b=[100, 202]，a[0]先和b[0]比较，6<100，小的值存在c，即c[0]=6，同时释放a[0]。若a[0]>b[0]，b[0]将会存储在c，释放的值将是b[0]，此时a和b均还有元素，则下一个将是a[0]与b[1]比较。以此类推，直到a或b其中一方释放完，另外一方剩下的有序数组的元素值肯定比c要大，所以可以和c合并，排在c后面

#### 优点：
  - 归并排序是稳定的排序，即相等的元素的顺序不会改变
  - 这对要排序数据包含多个信息而要按其中的某一个信息排序，要求其它信息尽量按输入的顺序排列时很重要
  - 一般用于对总体无序，但是各子项相对有序的数列

#### PHP实现：
{% highlight php startinline %}
<?php
    function al_merge_sort($arr){
        $len = count($arr);
        if($len <= 1){
            return $arr;//当数组拆剩一个元素时，递归结束条件，返回给$left_arr／$right_arr，然后执行al_merge函数
        }
        $mid = intval($len/2);//取数组长度中间值，保留整数部分，相当于向下取整
        $left_arr = array_slice($arr, 0, $mid);//拆分数组0-mid这部分给左边left_arr
        $right_arr = array_slice($arr, $mid);//拆分数组mid-末尾这部分给右边right_arr
        $left_arr = al_merge_sort($left_arr);//左边拆分完后开始递归合并往上走
        $right_arr = al_merge_sort($right_arr);//右边拆分完毕开始递归往上走
        $arr = al_merge($left_arr, $right_arr);//合并两个数组，继续递归
        return $arr;
    }

   function al_merge($arrA,$arrB)
   {
       $arrC = array();
      //这里不断的判断哪个值小，就将小的值给到arrC，到最后不是剩下arrA就是剩下arrB里的有序值，且肯定比arrC里面所有的值都大
       while(count($arrA) && count($arrB)){
           $arrC[] = $arrA['0'] < $arrB['0'] ? array_shift($arrA) : array_shift($arrB);
       }
       return array_merge($arrC, $arrA, $arrB);
   }

   $arr = array(12, 5, 4, 7, 8, 3, 4, 2, 6, 4, 9);
   print_r(al_merge_sort($arr));
{% endhighlight %}

#### 参考资料：
##### [归并排序_百度百科](https://baike.baidu.com/item/%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F/1639015)