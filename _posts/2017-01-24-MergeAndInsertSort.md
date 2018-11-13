---
layout: post
title: 归并排序和插入排序的几种实现以及算法效率比较
subtitle: 归并排序中嵌入插入排序
date: 2017-01-24 17:52:05
author: "Jerry"
catalog:    true
header-img: "img/home-bg-o.jpg"
tags:
    - 算法导论
    - 排序算法
---

> 根据算法导论第二章内容以及习题，编写了归并排序，插入排序（包括折半插入排序），递归版的插入排序，归并排序（小数组用插入排序进行），并比较其算法效率。

## 归并排序（二路归并）

归并排序基于分治策略，既然是分治策略必然有三个步骤
- **分解**：将含有n个元素的待排序部分先划分为两子序列，分别含有n/2个元素
- **解决**：使用归并排序递归地排序两个子序列
- **合并**：合并两个已排序的子序列以产生已排序的序列

```java
public void merge_sort(int[] A, int p, int r){
    if(p<r){
        int q = (p+r)/2;
        merge_sort(A,p,q);
        merge_sort(A,q+1,r);
        merge(A,p,q,r);
    }
}

public void merge(int[] A, int p, int q, int r){
    int[] L = new int[q-p+1];
    int[] R = new int[r-q];
    for(int i=0;i<L.length;i++){L[i]=A[p+i];}
    // print_array(L);
    for(int i=0;i<R.length;i++){R[i]=A[q+i+1];}
    // print_array(R);
    //注意A数组从K开始
    int i = 0, j = 0, k=p;
    while(i<L.length&&j<R.length){
        if(L[i]>R[j]){
            A[k++] = R[j++];
        }else{
            A[k++] = L[i++];
        }
    }
    while(i<L.length)A[k++] = L[i++];
    while(j<R.length)A[k++] = R[j++];
}
```

## 插入排序

```java
public void inserSort(int[] a){
    int len = a.length;
    for(int j=1;j<len;j++){
        int key = a[j];
        int i = j-1;
        while(i>=0&&a[i]>key){
            a[i+1]=a[i];
            i--;
        }
        a[i+1]=key;
    }
}
```


## 折半插入排序

```java
 public void insert_sort(int[] A){
    for(int i = 1;i<A.length;i++){
        int key = A[i];
        //折半插入
        int low = 0, high = i - 1;
        //这里一定是小于等于号，因为low==high时也要判断该数是否比key值大
        while(low<=high){
            int mid = (low + high)/2;
            if(A[mid]>key){
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }
        //待插入位置为high+1，将元素后移
        for(int k = i-1;k>high;k--){A[k+1] = A[k];}
        A[high+1] = key;
    }
}
```

## 采用递归的插入排序

算法导论书上练习题2.3-4，当数组长度超过一定值（100000的时候就栈溢出了），**容易栈溢出**。

```java
public void recursionInsertSort(int[] A, int p, int r){
    if(p<r){
        --r;
        recursionInsertSort(A,p,r);
        inserSort(A,p,r);
    }
}

//将数组A的下标r的数插入到数组中去，p~r-1为有序的
public void insert(int[] A, int p, int r){
    int key = A[r], k = r-1;
    for(;k>=p&&A[k]>key;k--)A[k+1] = A[k];
    A[k + 1] = key;
}
```

## 归并排序中嵌入插入排序

算法导论书上思考题2-1，当序列中**数字个数少于k的时候用插入排序**，而不是一直归并到序列中所含的数为一。

```java
//k题目中的k，使用插入排序的阙值
public void merge2_sort(int[] A, int p, int r, int k){
    if(r-p>k){
        int q = (p+r)/2;
        merge2_sort(A,p,q,k);
        merge2_sort(A,q+1,r,k);
        merge(A,p,q,r);
    }else{
        insert_sort_for_merge(A,p,r);
    }
}

public void insert_sort_for_merge(int[] A, int p, int r){
    for(int i = p + 1;i <= r;i++){
        int key = A[i];
        int low = p, high = i - 1;
        //这里一定是小于等于号，因为low==high时也要判断该树是否比key值大
        while(low<=high){
            int mid = (low + high)/2;
            if(A[mid]>key){
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }
        for(int k = i-1;k>high;k--)A[k+1] = A[k];
        A[high + 1] = key;
    }
}
```

## 效率比较（主要比较归并排序和改进过的归并排序）

1. 当数组长度为100000左右时，两者效率差不多
2. 当数组长度为1000000时，改进过的归并排序要快300ms。
3. 当数组长度为10000000时，改进过的归并排序和原始的排序不相上下，取决于改进归并排序中k的取值

