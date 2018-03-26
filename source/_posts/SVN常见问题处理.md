---
title: SVN常见问题处理
date: 2017-09-15 10:03:20
tags: SVN
---

### 一、Merge操作时，选择合并的修订弹窗加载非常慢

### 1.1、解决方案：
```
Settings -> Advanced -> LogFindCopyFrom: set to false
```
### 二、文件状态图标经常不能实时更新

### 2.1、解决方案：
```
Settings->Icon Overlays->Status cache选择none->应用->确定
```

