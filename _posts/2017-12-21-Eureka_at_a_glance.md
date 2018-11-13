---
layout: post
title: Leetcode-389-390
date: 2017-12-21 09:10:01
catalog:    true
author: "Jerry"
header-img: "img/green.png"
tags: 
    - LeetCode
---
# Eureka 初见

    该文章属于译文，[原文](https://github.com/Netflix/eureka/wiki/Eureka-at-a-glance)

## 什么是Eureka

Eureka是基于REST（Representational State Transfer, 表述性状态转移）的服务，主要被用来AWS云上定位服务，以实现中间层服务器的负载均衡，故障转移。我们把这种服务称作Eureka服务器。Eureka还带有一个基于java的客户端组件，即Eureka客户端，它使得服务间通信变得更为简单。Eureka客户端还内置了负载均衡器，可以进行基本的循环负载均衡。在Netflix中，一个更为复杂的负载均衡器装入Eureka中，提供基于几个因子，例如流量，资源使用邱凯，错误条件等的加权负载均衡，以提供卓越的弹性（即负载均衡变为更可控，可以根据需求进行调整）。

## Eureka的需求是什么

在AWS云中，由于其固有的特点，服务器来来去去。不像传统负载均衡器使用已知的IP地址和主机名的服务器，在AWS中，负载均衡需要更加复杂的注册和取消注册的负载均衡服务器。因为AWS尚未提供一个负载均衡中间件，Eureka填补了中间层负载平衡领域的巨大空白。
## Eureka和AWS ELB的不同之处

## Eureka和Route 53的不同之处

## 在Netflix中如何使用Eureka

## 什么时候需要使用Eureka

## 应用客户端和应用服务器端是如何通信的

## 高可用架构
