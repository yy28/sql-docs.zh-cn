---
title: 转换 Python 和 SQL 数据类型
description: 查看数据科学和机器学习解决方案中 Python 和 SQL Server 之间的隐式和显式数据类型转换。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/30/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ee493ec09c5cfc8a5198239cd5cafcb2579f50d8
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178610"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python 与 SQL Server 之间的数据类型映射
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

对于在 SQL Server 机器学习服务中的 Python 集成功能上运行的 Python 解决方案，请查看不支持的数据类型列表，以及在 Python 和 SQL Server 之间传递数据时可能隐式执行的数据类型转换。

## <a name="python-version"></a>Python 版本

RevoScaleR 功能的子集（rxLinMod、rxLogit、rxPredict、rxDTrees、rxBTrees，可能还有一些其他功能）是使用 Python API（使用一个新的 Python 包“revoscalepy”）提供的  。 可以通过此包使用 Pandas 数据帧、XDF 文件或 SQL 数据查询来处理数据。

有关详细信息，请参阅 [SQL Server 中的 revoscalepy 模块](ref-py-revoscalepy.md)和 [revoscalepy 函数参考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)。

与 SQL Server 相比，Python 支持的数据类型数量有限。 因此，每当在 Python 脚本中使用 SQL Server 中的数据时，数据都可能会隐式转换为兼容的数据类型。 但是，通常无法自动执行精确的转换并将返回错误。

## <a name="python-and-sql-data-types"></a>Python 和 SQL 数据类型

下表列出了提供的隐式转换。 不支持其他数据类型。

|SQLtype|Python 类型|说明
|-------|-----------|---------------------------------------------------------------------------------------------|
|**bigint**|`float64`|
|**binary**|`bytes`|
|**bit**|`bool`|
|**char**|`str`|
|**date**|`datetime`|
|**datetime**|`datetime`|支持 SQL Server 2017 CU6 及更高版本（具有 `datetime.datetime` 或 Pandas `pandas.Timestamp` 类型的 NumPy 数组 ）。 `sp_execute_external_script` 现在支持使用秒的小数形式的 `datetime` 类型。|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float64`|
|**smalldatetime**|`datetime`|
|**smallint**|`int32`|
|**tinyint**|`int32`|
|**uniqueidentifier**|`str`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**varchar(max)**|`str`|
