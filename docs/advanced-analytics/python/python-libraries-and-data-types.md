---
title: Python SQL 数据类型转换的 SQL Server 机器学习
description: 查看隐式和显式数据类型的 converstions Python 和 SQL Server 之间的数据科学和机器学习解决方案。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6a7cb7e8f93489bb52c1457fbf25bf7206026914
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642754"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Python 和 SQL Server 之间的数据类型映射
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

对于 Python 运行 SQL Server 机器学习服务中的 Python 集成功能的解决方案，查看不支持的数据类型和 Python 与 SQL Server 之间传递数据时可能会隐式执行的数据类型转换的列表。

## <a name="python-version"></a>Python 版本

SQL Server 2017 Anaconda 4.2 分发和 Python 3.6。

RevoScaleR 功能的子集 (rxLinMod，rxLogit，rxPredict，rxDTrees，rxBTrees，也许一些其他) 提供了使用 Python Api、 使用新的 Python 包**revoscalepy**。 此包可用于使用 Pandas 数据帧、 XDF 文件或 SQL 数据查询处理数据。

有关详细信息，请参阅[SQL Server 中的 revoscalepy 模块](ref-py-revoscalepy.md)并[revoscalepy 函数引用](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)。

Python 支持有限的数量的相比于 SQL Server 数据类型。 因此，只要使用从 SQL Server 在 Python 脚本中的数据，数据可能会隐式转换为兼容的数据类型。 但是，通常不能自动执行确切的转换，并且返回错误。

## <a name="python-and-sql-data-types"></a>Python 和 SQL 数据类型

此表列出了所提供的隐式转换。 不支持其他数据类型。

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

## <a name="see-also"></a>另请参阅

