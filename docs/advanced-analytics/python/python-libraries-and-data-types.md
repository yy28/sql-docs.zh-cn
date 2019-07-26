---
title: Python 到 SQL 数据类型转换
description: 查看数据科学和机器学习解决方案中 Python 与 SQL Server 之间的隐式和显式数据类型 converstions。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8aea7e67f6560aa750e67601b5b6a41f7d68b47d
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470338"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python 与 SQL Server 之间的数据类型映射
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

对于在 SQL Server 机器学习服务中的 Python 集成功能上运行的 Python 解决方案, 请查看不支持的数据类型的列表, 以及在 Python 和 SQL Server 之间传递数据时可能隐式执行的数据类型转换。

## <a name="python-version"></a>Python 版本

SQL Server 2017 Anaconda 4.2 分发版和 Python 3.6。

使用 Python Api (rxLinMod、rxLogit、rxPredict、rxDTrees、rxBTrees, 可能还有一些其他功能) 提供 RevoScaleR 功能的**子集。** 可以使用此包处理使用 Pandas 数据帧、XDF 文件或 SQL 数据查询的数据。

有关详细信息, 请参阅 SQL Server 和[revoscalepy 函数参考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)[中的 revoscalepy 模块](ref-py-revoscalepy.md)。

与 SQL Server 相比, Python 支持的数据类型数量有限。 因此, 当你在 Python 脚本中使用来自 SQL Server 的数据时, 数据可能会隐式转换为兼容的数据类型。 但是, 通常不能自动执行精确转换, 而是返回错误。

## <a name="python-and-sql-data-types"></a>Python 和 SQL 数据类型

下表列出了提供的隐式转换。 不支持其他数据类型。

|SQLtype|Python 类型|
|-------|-----------|
|**bigint**|`numeric`|
|**binary**|`raw`|
|**bit**|`bool`|
|**char**|`str`|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float32`|
|**smallint**|`int16`|
|**tinyint**|`uint8`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**varchar(max)**|`str`|

## <a name="see-also"></a>请参阅

