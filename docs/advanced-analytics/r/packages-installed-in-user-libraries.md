---
title: 使用用户库-SQL Server 机器学习服务中安装的 R 包的提示
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ee5dc9dc8b1730f26bada915d739f164a884801d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510774"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>在 SQL Server 中使用 R 包的提示
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

这篇文章的 Dba，他们不熟悉 R 和有经验的 R 开发人员不熟悉的包访问 SQL Server 实例中有单独的部分。

## <a name="new-to-r"></a>不熟悉 R

以管理员身份安装 R 包第一次，了解有关 R 包管理的一些基本知识可帮助你立即开始。

### <a name="package-dependencies"></a>包的依赖项

R 包通常依赖于多个其他包，其中一些可能不可用的实例使用的默认 R 库中。 有时包所要求不同版本的已安装的依赖包。 包的依赖项记录在包中，嵌入到说明文件中，但有时不完整。 可以使用名为的包[iGraph](https://igraph.org/r/)以清楚地表述了依赖项关系图。

如果你需要安装多个包，或想要确保你的组织中的每个人都会获得正确的包类型和版本，我们建议你使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)包来分析完整的依赖关系链。 minicRAN 创建本地存储库，可以在多个用户或计算机之间共享。 有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

### <a name="package-sources-versions-and-formats"></a>包源、 版本和格式

有多个来源获取 R 包，如[CRAN](https://cran.r-project.org/)并[请](https://www.bioconductor.org/)。 R 语言官方站点 (<https://www.r-project.org/>) 列出了许多这些资源。 Microsoft 提供了[MRAN](https://mran.microsoft.com/)对于其分布的开放源代码 R ([MRO](https://mran.microsoft.com/open)) 和其他包。 许多包发布到 GitHub，开发人员可从中获取源代码。

在多个计算平台上运行的 R 包。 请确保你安装的版本的 Windows 二进制文件。

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>知道将安装到的库和已安装的包。

如果你之前修改的计算机上，在 R 环境安装任何内容之前，确保 R 环境变量`.libPath`使用只是一个路径。

此路径应指向实例的 R_SERVICES 文件夹。 有关详细信息，包括如何确定已安装的包，请参阅[SQL Server 中的默认 R 和 Python 包](installing-and-managing-r-packages.md)。

## <a name="new-to-sql-server"></a>刚接触 SQL Server

作为 R 开发人员致力于 SQL Server 上执行的代码，保护服务器的安全策略限制你能够控制 R 环境。

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 用户库： 不支持 SQL Server 上

R 开发人员需要安装新的 R 包习惯于安装的包，随意情况下，只要默认库不可用，或者当开发人员不是计算机上的管理员使用专用的、 用户库。 例如，在典型的 R 开发环境，用户将添加的包的位置到 R 环境变量`libPath`，或者引用完整的包路径，如下：

```R
library("c:/Users/<username>/R/win-library/packagename")
```

这不会工作，在 SQL Server 中运行 R 解决方案时因为必须将 R 包安装到与该实例相关联的特定默认库。 包的默认库中不可用，你会收到此错误，当你尝试调用包时：

*库 （xxx） 中的错误： 没有名为包名称的包*

### <a name="avoid-package-not-found-errors"></a>避免出现"找不到包"错误

+ 消除用户库上的依赖项。 

    则会导致错误，如果由另一个用户不能访问到库位置运行解决方案，它是所需的 R 包安装到自定义用户库，错误开发做法。

    此外，如果默认库中安装包，R 运行时加载包从默认库中，即使 R 代码中指定了其他版本。

+ 修改代码以在共享环境中运行。

+ 避免为解决方案的一部分安装的包。 如果您没有安装包的权限，代码将失败。 即使您有权安装包，您应单独执行操作因此从你想要执行的其他代码。

+ 检查代码以确保未调用已卸载的包。

+ 更新代码以删除对 R 包或 R 库的路径直接引用。 

+ 知道哪些包库是与实例相关联。 有关详细信息，请参阅[SQL Server 中的默认 R 和 Python 包](installing-and-managing-r-packages.md)。

## <a name="see-also"></a>另请参阅

+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)