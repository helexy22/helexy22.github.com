---
layout:     post   				    # 使用的布局（不需要改）
title:     算法样例测试模块-01 				# 标题 
subtitle:   适用于数组的样式操作  #副标题
date:       2020-01-10 				# 时间
author:     helexy22 						# 作者
# header-img: img/post-bg-2015.jpg  #这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Algorithm
---

### 生成随机数组

```java
// maxSize
// maxValue
public static int[] generateRandomArray(int maxSize, int maxValue) {
		int[] arr = new int[(int) ((maxSize + 1) * Math.random())];
		for (int i = 0; i < arr.length; i++) {
			arr[i] = (int) ((maxValue + 1) * Math.random()) - (int) (maxValue * Math.random());
		}
		return arr;
	}
```

### 结果打印

```java
// arr
public static void printArray(int[] arr) {
    if (arr == null) {
        return;
    }
    for (int i = 0; i < arr.length; i++) {
        System.out.print(arr[i] + " ");
    }
    System.out.println();
}
```


### 自带的排序

```java
// arr
public static void comparator(int[] arr) {
		Arrays.sort(arr);
	}
```

### 比较两个数组,对数器


```java
// arr1
// arr2
public static boolean isEqual(int[] arr1, int[] arr2) {
    if ((arr1 == null && arr2 != null) || (arr1 != null && arr2 == null)) {
        return false;
    }
    if (arr1 == null && arr2 == null) {
        return true;
    }
    if (arr1.length != arr2.length) {
        return false;
    }
    for (int i = 0; i < arr1.length; i++) {
        if (arr1[i] != arr2[i]) {
            return false;
        }
    }
    return true;
}

```