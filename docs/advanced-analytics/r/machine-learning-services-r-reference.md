---
title: "对 SQL Server 机器学习服务的 API 参考 |Microsoft 文档"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1c776c43d66d01a2f721b5d3d8bc540741bf8b13
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---

# <a name="api-reference-for-sql-server-machine-learning-services"></a>对 SQL Server 机器学习服务的 API 参考

本文提供了机器学习 SQL Server 使用的 Api 的参考文档的链接。 

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

大多数情况下，SQL Server 使用相同 Microsoft R Server 和 Microsoft 机器学习 Server 中提供的 R 和 Python 库。 

> [!NOTE]
> 对于所有的 Api 文档派生自源代码，并且不后编辑。

## <a name="r"></a>R

+ [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

    支持远程计算上下文和多个数据源的可缩放算法。

+ [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)

    。 需要 RevoScaleR 的学习算法和转换的快速且可伸缩的计算机。

+ [olapR](https://docs.microsoft.com/r-server/r-reference/olapr/olapr)

   读取 OLAP 数据源的架构，并执行 MDX 查询。

+ [sqlrutils](https://docs.microsoft.com/r-server/r-reference/sqlrutils/sqlrutils)

    用于从 R 代码生成格式正确的存储的过程的帮助程序函数。

+ [mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)

   用于在控制台应用程序建立远程会话和用于发布和管理 web 服务，它使用 R 或 Python 代码的函数。

## <a name="python"></a>Python

+ [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

    R 语言 RevoScaleR 包 Python 等效项。 支持的相同的计算上下文和数据源。

+ [Microsoftml for Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

    MicrosoftML Python 等效项相同的计算上下文和数据源，打包成。 支持，并包括快速、 可缩放的算法和从 Microsoft 的转换。

## <a name="related-apis"></a>相关的 Api

+ [RevoPEMAR 函数参考](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

    支持的并行算法的开发

+ [RevoUtils](https://docs.microsoft.com/r-server/r-reference/revoutils/revoutils)

    使用 RevoScaleR 环境使用的实用工具函数

## <a name="other"></a>其他

"帮助"主题和特定于使用的这些 R 或 SQL Server 中的 Python Api 的摘要可在此处找到：

+ [用于使用 SQL Server 的 scaleR 函数](scaler-functions-for-working-with-sql-server-data.md)
+ [生成存储的过程，请使用 sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
+ [读取到 R 使用 olapR 的 MDX 数据](how-to-create-mdx-queries-using-olapr.md)

