---
title: hi blog
date: 2018-03-14 13:54:49
tags:
---


# 私有Pods

refer to : [Cocoapods.org](https://guides.cocoapods.org/making/private-cocoapods)

## 1.在服务器或者GitHub创建私有spec仓库

```bash
$ mkdir SPECS_NAME
$ cd SPECS_NAME
$ git init --bare
```
<!-- more -->
## 2.本地将私有spec仓库添加到CocoaPods的安装

```bash
$ pod repo add REPO_NAME SPECS_SOURCE_URL
```

检查安装是否成功：
```bash
$ cd ~/.cocoapods/repos/REPO_NAME
$ pod repo lint .
```

## 3.把自己的Podspec添加到spec repo中

```bash
$ pod repo push REPO_NAME SPEC_NAME.podspec
```

示例JLRoutes.podspec文件：
```ruby
Pod::Spec.new do |s|
  s.name         = "JLRoutes"
  s.version      = "2.1"
  s.summary      = "URL routing library for iOS with a simple block-based API."
  s.homepage     = "https://github.com/joeldev/JLRoutes"
  s.license      = "BSD 3-Clause \"New\" License"
  s.author       = { "Joel Levin" => "joel@joeldev.com" }
  s.source       = { :git => "https://github.com/joeldev/JLRoutes.git", :tag => "2.1" }
  s.framework    = 'Foundation'
  s.requires_arc = true

  s.source_files = 'JLRoutes', 'JLRoutes/*.{h,m}', 'JLRoutes/Classes/*.{h,m}'

  s.ios.deployment_target = '8.0'
  s.osx.deployment_target = '10.10'
  s.tvos.deployment_target = '9.0'
end
```

## 4.使用私有的pod

```ruby
source 'SPECS_SOURCE_URL'
```

如果同时要使用Cocoapods的默认source

```ruby
source 'https://github.com/CocoaPods/Specs.git'
```
### [!] The repo `ppy-specs` at `.` is not clean

> 即使是.gitignore文件也不能存在，ppy-specs文件夹必须保证绝对干净。
