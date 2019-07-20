---
title: 有关使用安装在用户库中的 R 包的技巧
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a03d78e5d3100105f74e2efe361391a6bcfaf7ac
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345277"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>在 SQL Server 中使用 R 包的技巧
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文为 Dba 提供了单独的部分, 这些读者不熟悉 R 和经验丰富的 R 开发人员, 这些开发人员不熟悉 SQL Server 实例中的包访问。

## <a name="new-to-r"></a>R 新手

作为首次安装 R 包的管理员, 了解有关 R 包管理的几个基础知识可以帮助你入门。

### <a name="package-dependencies"></a>包依赖关系

R 包经常依赖于多个其他包, 其中一些包可能在实例使用的默认 R 库中不可用。 有时, 包需要已安装的不同版本的依赖包。 包依赖项记录在包中嵌入的说明文件中, 但有时不完整。 可以使用名为[iGraph](https://igraph.org/r/)的包来完全表述依赖项关系图。

如果需要安装多个包, 或者想要确保组织中的每个人都获得正确的包类型和版本, 我们建议使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)包分析完整的依赖关系链。 minicRAN 创建可在多个用户或计算机之间共享的本地存储库。 有关详细信息, 请参阅[使用 MiniCRAN 创建本地包存储库](create-a-local-package-repository-using-minicran.md)。

### <a name="package-sources-versions-and-formats"></a>包源、版本和格式

R 包有多个源, 例如[CRAN](https://cran.r-project.org/)和[Bioconductor](https://www.bioconductor.org/)。 R 语言的官方站点 (<https://www.r-project.org/>) 列出了许多这样的资源。 Microsoft 为开源 R ([MRO](https://mran.microsoft.com/open)) 和其他包的发行版提供了[MRAN](https://mran.microsoft.com/) 。 许多包发布到 GitHub, 开发人员可在其中获取源代码。

R 包在多个计算平台上运行。 确保安装的版本为 Windows 二进制文件。

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>了解要安装到的库以及已安装的包。

如果你之前在计算机上修改了 R 环境, 则在安装任何组件之前, 请确保 R 环境`.libPath`变量只使用一个路径。

此路径应指向实例的 R_SERVICES 文件夹。 有关详细信息, 包括如何确定哪些包已安装, 请参阅[SQL Server 中的默认 R 和 Python 包](../package-management/default-packages.md)。

## <a name="new-to-sql-server"></a>SQL Server 的新

作为 R 开发人员处理 SQL Server 上执行的代码, 保护服务器的安全策略会限制你控制 R 环境的能力。

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 用户库: 在 SQL Server 上不受支持

需要安装新的 R 包的 r 开发人员习惯于安装中的包, 只要默认库不可用, 或者当开发人员不是计算机的管理员时, 将使用专用的用户库。 例如, 在典型的 R 开发环境中, 用户会将包的位置添加到 R 环境变量`libPath`, 或引用完整的包路径, 如下所示:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

在 SQL Server 中运行 R 解决方案时, 此功能不起作用, 因为 R 包必须安装到与实例关联的特定默认库。 如果包在默认库中不可用, 则在尝试调用包时, 会收到此错误:

*库中的错误 (xxx): 不存在名为 "package-name" 的包*

### <a name="avoid-package-not-found-errors"></a>避免 "找不到包" 错误

+ 消除对用户库的依赖。 

    将所需的 R 包安装到自定义用户库是一种不好的开发做法, 因为如果某个解决方案由不具有库位置访问权限的其他用户运行, 则会导致错误。

    此外, 如果在默认库中安装了包, 则 R 运行时将从默认库加载包, 即使在 R 代码中指定了其他版本也是如此。

+ 修改您的代码以在共享环境中运行。

+ 避免将包安装为解决方案的一部分。 如果你没有安装包的权限, 则代码将失败。 即使您具有安装包的权限, 您也应该单独从要执行的其他代码执行此操作。

+ 检查代码以确保未调用已卸载的包。

+ 更新代码以删除对 R 包或 R 库路径的直接引用。 

+ 了解与实例关联的包库。 有关详细信息, 请参阅[SQL Server 中的默认 R 和 Python 包](../package-management/default-packages.md)。

## <a name="see-also"></a>请参阅

+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)