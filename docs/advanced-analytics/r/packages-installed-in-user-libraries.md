---
title: "避免错误上安装的用户库中的 R 程序包 |Microsoft 文档"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 0de06ebee16d903b4b00c9d8e4673bf450c485d1
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>避免在用户库中安装的 R 包上的错误

有经验的 R 用户习惯于在用户库中，安装 R 包，默认库时被阻止或不可用。 但是，此方法不支持在 SQL Server，并且安装到用户库通常以"找不到包"错误。

本主题提供解决方法可帮助您避免此错误。 本文档说明如何修改 R 代码，并提供有关使用从 SQL Server 实例的 R 包的正确 R 包安装进程的建议。

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>为什么不能 R 用户库从 SQL Server 访问

R 开发人员需要安装新的 R 包都习惯于安装随意情况下，此包和只要默认库不可用，或者当开发人员不是计算机上的管理员使用专用的用户库。

例如，在典型的 R 开发环境中，用户将添加包的位置的 R 环境变量`libPath`，或引用的完整包路径，如下：

```R
library("c:/Users/<username>/R/win-library/packagename")  
```

但是，这可以永远不会处理在 SQL Server 中运行 R 解决方案时因为 R 包必须安装到与实例关联的特定的默认库。

如果包未安装到默认库中，则在尝试调用该包时，可能会收到以下错误：

*Library(xxx) 时出错： 没有名为包-name 的包*

还有一种错误开发做法将所需的 R 包安装到自定义用户的库，因为它将导致错误，如果由不到库位置具有访问另一个用户运行解决方案。

## <a name="how-to-install-r-packages-to-an-accessible-library"></a>如何将 R 包安装到访问的库

**有关 SQL Server 2016**

使用与实例关联的包库。 有关详细信息，请参阅[与 SQL Server 安装的 R 包](installing-and-managing-r-packages.md)

**SQL server 自 2017 年 1**

SQL Server 提供功能，可帮助你管理多个包版本，并对其授予用户权限单个包，而无需用户具有文件系统访问权限。

有关如何设置共享的包库并将用户分配到角色的详细信息，请参阅[for SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)。

如果要基于数据库角色的包管理方法，则不需要在不同的用户目录中安装的同一个包的多个副本。 安装单个包副本的需要并且与经过身份验证的用户共享。 因为在数据库级别管理包，你还可以复制的包和数据库之间的相关的权限的组。

## <a name="tips-for-avoiding-package-not-found-errors"></a>为避免"找不到包"错误的提示

+ 修改代码以消除用户库上的依赖关系。 当你将在迁移运行的 R 解决方案[!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)]，务必你执行以下操作：

    + 将所需的任何包安装到与实例关联的默认库。

    + 编辑代码以确保从默认库中，不是从临时目录或用户库加载包。

+ 避免作为解决方案的一部分的即席包安装。 检查代码以确保有到安装的包或动态安装包的代码不调用。 如果您没有权限，代码将失败，并且如果您具有权限，你应该从你想要执行的其他代码单独安装包。

+ 修改任何直接对 R 包库路径。 如果包安装在默认库中，则 R 运行时将从默认库加载包，即使 R 代码中指定了不同的库也是如此。

