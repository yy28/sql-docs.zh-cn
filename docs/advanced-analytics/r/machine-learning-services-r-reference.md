---
title: 对 SQL Server 机器学习服务的 API 参考 |Microsoft 文档
ms.custom: ''
ms.date: 10/31/2017
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
ms.openlocfilehash: 77f0e3af1281cd4f6249defff820ccb7b7f5f238
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="api-reference-for-sql-server-machine-learning-services"></a>对 SQL Server 机器学习服务的 API 参考
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供了机器学习 SQL Server 使用的 Api 的参考文档的链接。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

大多数情况下，SQL Server 使用相同 Microsoft R Server 和 Microsoft 机器学习 Server 中提供的 R 和 Python 库。 

> [!NOTE]
> 所有 Api 文档派生自源代码并不编辑。 如果你看到错误，请添加注释中的 API 参考文档。 

## <a name="r"></a>R

+ [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

    支持远程计算上下文和多个数据源的可缩放算法。

+ [MicrosoftML](https://docs.microsoft.com/machine-learning-serverr-reference/microsoftml/microsoftml-package)

    。 需要 RevoScaleR 的学习算法和转换的快速且可伸缩的计算机。

+ [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)

   读取 OLAP 数据源的架构，并执行 MDX 查询。

+ [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)

    用于从 R 代码生成格式正确的存储的过程的帮助程序函数。

+ [mrsdeploy](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)

   用于在控制台应用程序建立远程会话和用于发布和管理 web 服务，它使用 R 或 Python 代码的函数。

## <a name="python"></a>Python

+ [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)

    R 语言 RevoScaleR 包 Python 等效项。 支持的相同的计算上下文和数据源。

+ [Microsoftml for Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)

    MicrosoftML Python 等效项相同的计算上下文和数据源，打包成。 支持，并包括快速、 可缩放的算法和从 Microsoft 的转换。 

## <a name="related-apis"></a>相关的 Api

+ [RevoPEMAR 函数参考](https://docs.microsoft.com/machine-learning-server/r-reference/revopemar/pemar)

    支持的并行算法的开发

+ [RevoUtils](https://docs.microsoft.com/machine-learning-server/r-reference/revoutils/revoutils)

    使用 RevoScaleR 环境使用的实用工具函数

## <a name="other"></a>其他

"帮助"主题和特定于使用的这些 R 或 SQL Server 中的 Python Api 的摘要可在此处找到：

+ [用于使用 SQL Server 的 scaleR 函数](scaler-functions-for-working-with-sql-server-data.md)
+ [生成存储的过程，请使用 sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
+ [读取到 R 使用 olapR 的 MDX 数据](how-to-create-mdx-queries-using-olapr.md)
