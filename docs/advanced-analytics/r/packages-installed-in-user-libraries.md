---
title: 使用安装的 SQL Server 上的用户库中的 R 程序包的提示 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e52a6f4a9a3830aab01e54819804785a7069c9d2
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34708465"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>在 SQL Server 中使用 R 包的技巧
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文为不熟悉 R 和有经验的 R 开发人员熟悉的包中的 SQL Server 实例的访问权限的 Dba 有单独的章节。

## <a name="new-to-r"></a>新手 R

以管理员身份安装 R 包第一次，但是知道有关 R 包管理的几个基础知识可以帮助你为开始。

### <a name="package-dependencies"></a>包的依赖项

R 包经常依赖于多个其他包，其中一些可能不可用的实例所使用的默认 R 库中。 有时包需要已安装的从属包的不同版本。 包的依赖项在包中嵌入的描述文件中说明，但它只是有时不完整。 在可以使用调用的包[iGraph](http://igraph.org/r/)以清楚地表述了依赖项关系图。

如果你需要安装多个包，或想要确保你的组织中的每个人都获得正确的包类型和版本，我们建议你使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)包以分析完成的依赖关系链。 minicRAN 创建可以在多个用户或计算机之间共享的本地存储库。 有关详细信息，请参阅[创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

### <a name="package-sources-versions-and-formats"></a>包源、 版本和格式

如有多个来源获取 R 包， [CRAN](https://cran.r-project.org/)和[Bioconductor](https://www.bioconductor.org/)。 R 语言官方站点 (<https://www.r-project.org/>) 列出了很多这些资源。 Microsoft 提供了[MRAN](https://mran.microsoft.com/)对于其分布的开放源代码 R ([MRO](https://mran.microsoft.com/open)) 和其他包。 很多包发布到 GitHub，开发人员可以从何处获取源代码。

在多个计算平台上运行的 R 程序包。 请确保你安装的版本是 Windows 二进制文件。

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>知道要安装到的库和已安装的包。

如果以前已修改的 R 环境的计算机上，在安装任何内容之前，确保 R 环境变量`.libPath`使用一个路径。

此路径应指向实例 R_SERVICES 文件夹。 有关详细信息，包括如何确定哪些包已安装，请参阅[SQL Server 中的默认 R 和 Python 包](installing-and-managing-r-packages.md)。

## <a name="new-to-sql-server"></a>新到 SQL Server

作为 R 开发人员处理在 SQL Server 上执行的代码，保护服务器的安全策略来限制你能够控制 R 环境。

### <a name="r-user-libraries-not-supported-on-sql-server"></a>R 用户库： 不支持在 SQL Server 上

R 开发人员需要安装新的 R 包都习惯于安装包随意情况下，只要默认库不可用，或者当开发人员不是计算机上的管理员使用专用的、 用户库。 例如，在典型的 R 开发环境中，用户将添加包的位置的 R 环境变量`libPath`，或引用的完整包路径，如下：

```R
library("c:/Users/<username>/R/win-library/packagename")
```

这不在 SQL Server 中运行 R 解决方案时，因为工作不到与实例关联的特定的默认库必须安装 R 包。 包中的默认库不可用，将会获得此错误，当你尝试调用包时：

*Library(xxx) 时出错： 没有名为包-name 的包*

### <a name="avoid-package-not-found-errors"></a>避免"找不到包"错误

+ 取消用户库上的依赖关系。 

    错误开发做法若要将所需的 R 包安装到自定义用户的库，是因为它将导致错误，如果由不到库位置具有访问另一个用户运行解决方案。

    此外，如果默认库中安装包，R 运行时加载包从默认库中，即使在 R 代码中指定其他版本。

+ 修改你的代码在共享环境中运行。

+ 避免作为解决方案的一部分安装包。 如果你没有安装包的权限，代码将失败。 即使您具有权限，安装包，你应单独执行操作因此从你想要执行的其他代码。

+ 检查代码以确保未调用已卸载的包。

+ 更新代码以删除对 R 包或 R 库路径直接引用。 

+ 知道哪个包库是与实例关联。 有关详细信息，请参阅[SQL Server 中的默认 R 和 Python 包](installing-and-managing-r-packages.md)。

## <a name="see-also"></a>另请参阅

+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)