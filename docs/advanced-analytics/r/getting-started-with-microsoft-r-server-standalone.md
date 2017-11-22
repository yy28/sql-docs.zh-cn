---
title: "Microsoft R Server（独立版）入门 | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: a0932e10c72166bee4b674ea5df6e80b032e7964
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="getting-started-with-machine-learning-server-standalone"></a>机器学习 Server （独立版） 入门
 
在 SQL Server 2016，Microsoft R Server （独立） 帮助将受欢迎的开源 R 语言引入企业，若要启用高性能分析解决方案以及与其他业务应用程序集成。  

在 SQL Server 自 2017 年 1，名称已更改为机器学习 Server （独立） 以反映的 Python 语言的支持添加。 这两个版本都可免费用于 Enterprise Edition 或软件保障实现的用户。

本文提供了如何使用机器学习服务器 （或 R Server），以及如何安装和示例入门的高级概述。

## <a name="why-use-a-standalone-server-for-machine-learning"></a>为什么将独立服务器用于机器学习

如果你不需要集成机器学习使用 SQL Server 数据的解决方案，机器学习服务器提供的 R 和 Python，同一分布式、 可缩放的支持，并此外支持部署到 Hadoop、 Spark 中或 Linux 的解决方案。

机器学习服务器还包括图像分析和观点分析，则可以立即使用应用程序中预先训练的模型。

机器学习服务器的操作化功能支持部署和分发 R 和 Python 解决方案通过 web 服务使用远程执行的 Spark 和 Hadoop MapReduce 群集拓扑，以及支持 Windows 或 Linux。

**SQL Server 2016**

+ 从 SQL Server 2016 安装程序安装 Microsoft R Server （独立）。

    此选项创建的独立服务器，都完全独立于在 R Services （数据库）。 此版本仅支持 R。 在 SQL Server Enterprise Edition 支持策略中包括独立服务器安装程序。 有关详细信息，请参阅 [创建 R Server（独立版）](../../advanced-analytics/r/create-a-standalone-r-server.md)。

+ 安装 R Server 使用单独的 Windows installer。

    此安装程序创建使用 Microsoft 现代软件生命周期支持策略的 Microsoft R Server 的新实例。 此外可以安装 R Server Linux、 Cloudera、 Teradata，和 Hadoop。
    
    有关详细信息，请参阅[适用于 Windows 中安装 R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

**SQL Server 2017**

+ 从 SQL Server 2017 安装程序安装机器学习 Server （独立）。 

    此选项创建的独立服务器以支持的机器学习中 R 和 / 或 Python，操作化的。 在 SQL Server Enterprise Edition 支持策略中包括独立服务器安装程序。 有关详细信息，请参阅 [创建 R Server（独立版）](../../advanced-analytics/r/create-a-standalone-r-server.md)。  

+ 使用新的独立 Windows 安装程序。

    此安装方法创建使用 Microsoft 现代软件生命周期支持策略的机器学习服务器的新实例。 此外可以在 Hadoop、 Spark 中或 Linux 上安装机器学习服务器，且不另外收费。
    
    有关详细信息，请参阅[安装机器学习用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

**升级现有的服务器**

+ 如果你有现有的服务器或你想要升级的实例，下载并运行基于 Windows 的安装程序获取更新。 

    有关详细信息，请参阅[使用 SqlBindR 升级实例](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="start-using-machine-learning-server"></a>开始使用机器学习服务器

 已设置的服务器组件并配置你 IDE 使用机器学习服务器二进制文件之后，你可以开始开发使用新的 Api，如 RevoScaleR 和 revoscalepy、 MicrosoftML 和 olapR 解决方案。
    
若要开始，请参阅这些指南：

+ [解决方案模板](https://docs.microsoft.com/machine-learning-server/r/sample-solutions)

    这些示例是演示如何将应用在特定行业中的机器学习的解决方案。 当前的方案是在零售、 财务、 卫生保健和市场营销。

+ [浏览 R 和 25 函数中的 ScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)： 浏览提供高性能和缩放到 R 解决方案的可分发分析函数的此集合。 包括许多最流行的 R 建模包的可并行化版本，例如 K-均值聚类、决策树和决策林以及用于数据操作的工具。

- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx)

    MicrosoftML 包是机器的一套新学习算法和在 Microsoft 开发的快速且可伸缩的转换。 在 R 或 Python，可以使用它。 有关详细信息，请参阅[for Python MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)和[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)。

## <a name="see-also"></a>另请参阅

[Getting Started with SQL Server 机器学习服务](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)