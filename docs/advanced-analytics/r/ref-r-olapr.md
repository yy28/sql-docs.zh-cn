---
title: olapR R 函数库的 SQL Server 机器学习服务
description: 在 SQL Server 2016 R Services 和的 SQL Server 2017 机器学习服务中的 olapR 函数库介绍
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e5419900b8ba573ec0658a5022be68105b0b8607
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641854"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR （SQL Server 中的 R 库）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**olapR**是用于针对 SQL Server Analysis Services OLAP 多维数据集的 MDX 查询的 R 函数的 Microsoft 库。 函数不支持 MDX 的所有操作，但您可以生成该切片，切块，向下钻取，汇总，并对维度数据透视表的查询。 

此包不会预加载到 R 会话。 运行以下命令以加载库。

```R
library(olapR)
```

连接到所有受支持版本的 SQL Server 上的 Analysis Services OLAP 多维数据集，可以使用此库。 目前不支持连接到表格模型。

## <a name="package-version"></a>包版本

当前版本是 1.0.0 中所有的仅限 Windows 的产品，并下载提供库。

## <a name="full-reference-documentation"></a>完整的参考文档

**Olapr**库分布在多个 Microsoft 产品，但使用情况都是相同是否获取 SQL Server 或另一个产品中的库。 函数是相同的因为[单个 sqlrutils 函数的文档](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)发布到下一个位置[R 引用](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)的 Microsoft Machine Learning Server。 应任何特定于产品的行为存在，请将函数的帮助页中所示的差异。

## <a name="availability-and-location"></a>可用性和位置

在以下产品，以及 Azure 上的多个虚拟机映像提供了此包。 包位置会相应地有所不同。

产品 | Location |
--------|----------|
SQL Server 2017 机器学习服务 （使用 R 集成） | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Program Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Program Files\Microsoft\R Client\R_SERVER\library |
数据科学虚拟机 （在 Azure) | C:\Program Files\Microsoft\R Client\R_SERVER\library |
（Azure) 上的 SQL Server 虚拟机<sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> R 集成是可选的 SQL Server 中。 当在 VM 配置期间添加机器学习或 R 功能时，将安装 olapR 库。


## <a name="see-also"></a>另请参阅

[如何创建使用 olapR MDX 查询](how-to-create-mdx-queries-using-olapr.md)
