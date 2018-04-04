---
title: 避免错误上安装的用户库中的 R 程序包 |Microsoft 文档
titleSuffix: SQL Server
ms.custom: ''
ms.date: 02/20/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: a3498ca0940384dacf9f67ac916d78eee939f829
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>避免在用户库中安装的 R 包上的错误
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

有经验的 R 用户习惯于在用户库中，安装 R 包，默认库时被阻止或不可用。 但是，此方法不支持在 SQL Server，并且安装到用户库通常以"找不到包"错误。

本指南介绍了可帮助您避免此错误的解决方法。 本文档说明如何修改 R 代码，并提供有关使用从 SQL Server 实例的 R 包的正确 R 包安装进程的建议。

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>为什么不能 R 用户库从 SQL Server 访问

R 开发人员需要安装新的 R 包都习惯于安装包随意情况下，只要默认库不可用，或者当开发人员不是计算机上的管理员使用专用的、 用户库。

例如，在典型的 R 开发环境中，用户将添加包的位置的 R 环境变量`libPath`，或引用的完整包路径，如下：

```R
library("c:/Users/<username>/R/win-library/packagename")
```

这不在 SQL Server 中运行 R 解决方案时，因为工作不到与实例关联的特定的默认库必须安装 R 包。 包中的默认库不可用，将会获得此错误，当你尝试调用包时：

*Library(xxx) 时出错： 没有名为包-name 的包*

## <a name="how-to-avoid-package-not-found-errors"></a>如何避免"找不到包"错误

+ 取消用户库上的依赖关系 

    错误开发做法若要将所需的 R 包安装到自定义用户的库，是因为它将导致错误，如果由不到库位置具有访问另一个用户运行解决方案。

    此外，如果默认库中安装包，R 运行时加载包从默认库中，即使在 R 代码中指定的不同版本。

+ 修改你的代码在共享环境中运行。

+ 避免作为解决方案的一部分安装包。 如果你没有安装包的权限，代码将失败。 即使您具有权限，安装包，你应单独执行操作因此从你想要执行的其他代码。

+ 检查代码以确保未调用已卸载的包。

+ 更新代码以删除对 R 包或 R 库路径直接引用。 

+ 知道哪个包库是与实例关联。 有关详细信息，请参阅[与 SQL Server 安装的 R 包](installing-and-managing-r-packages.md)
