---
title: "Python 库 |Microsoft 文档"
ms.custom: 
ms.date: 03/30/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 6292b9139f4ad43a0bdd8de4b1d849cb0caaa627
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="python-libraries-and-data-types"></a>Python 库和数据类型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主题介绍以下产品附带的 Python 库：

+ SQL Server 机器学习服务 （数据库）
+ Microsoft 机器学习 Server （独立）

本主题还列出了不支持的数据类型和列表的数据类型转换可能会执行隐式当 Python 和 SQL Server 之间传递的数据。

## <a name="python-version"></a>Python 版本

SQL Server 自 2017 年 1 CTP 2.0 包含 Anaconda 分发和 Python 3.6 部分。

RevoScaleR 功能的子集 (rxLinMod，rxLogit，rxPredict，rxDTrees，rxBTrees，可能是几个其他人) 使用 Python API，使用新的 Python 包提供**RevoScalePy**。 你可以使用此包使用 Pandas 数据帧，处理数据。XDF 文件或 SQL 数据查询。

有关详细信息，请参阅[什么是 revoscalepy？](what-is-revoscalepy.md)。

## <a name="python-and-sql-data-types"></a>Python 和 SQL 数据类型

Python 支持有限的数量的相比于 SQL Server 数据类型。

因此，无论何时使用中的数据时，才[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Python 脚本，数据可能会隐式转换为兼容的数据类型。 但是，通常不能自动执行完全转换，并返回一个错误。

此表列出了提供的隐式转换。 不支持其他数据类型。

|SQLtype|Python 类型|
|-|-|
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
|**int**|`int16`|
|**tinyint**|`uint8`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**varchar(max)**|`str`|



