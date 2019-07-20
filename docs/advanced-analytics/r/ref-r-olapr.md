---
title: olapR R 函数库
description: SQL Server 2016 R Services 中的 olapR 函数库简介和 SQL Server 2017 机器学习服务 with R。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2363b9ba69f914f828d7445a88d6ee1c784bb096
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344878"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (SQL Server 中的 R 库)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**olapR**是一个用于针对 SQL Server Analysis Services OLAP 多维数据集的 MDX 查询的 R 函数的 Microsoft 库。 函数不支持所有 MDX 操作, 但可以生成对维度进行切片、切块、深化、汇总和透视的查询。 

此包未预加载到 R 会话中。 运行以下命令以加载库。

```R
library(olapR)
```

您可以使用此库连接到所有受支持版本的 SQL Server 上的 Analysis Services OLAP 多维数据集。 此时不支持连接到表格模型。

## <a name="package-version"></a>包版本

当前版本为 1.0.0, 适用于所有仅限 Windows 的产品和提供库的下载。

## <a name="full-reference-documentation"></a>完整参考文档

**Olapr**库分布在多个 Microsoft 产品中, 但不管你是在 SQL Server 还是在其他产品中获取库, 使用情况都是相同的。 由于函数相同, 因此,[每个 sqlrutils 函数的文档](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)仅发布到 Microsoft Machine Learning Server [R 引用](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)下的一个位置。 如果存在任何特定于产品的行为, 则函数帮助页中将注明差异。

## <a name="availability-and-location"></a>可用性和位置

以下产品以及 Azure 上的多个虚拟机映像中提供了此包。 包位置会相应地变化。

产品 | Location |
--------|----------|
SQL Server 2017 机器学习服务 (带 R 集成) | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Program Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Program Files\Microsoft\R Client\R_SERVER\library |
Data Science Virtual Machine (在 Azure 上) | C:\Program Files\Microsoft\R Client\R_SERVER\library |
SQL Server 虚拟机 (在 Azure 上) <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> R 集成在 SQL Server 中是可选的。 OlapR 库将在 VM 配置过程中添加机器学习或 R 功能时安装。


## <a name="see-also"></a>请参阅

[如何使用 olapR 创建 MDX 查询](how-to-create-mdx-queries-using-olapr.md)
