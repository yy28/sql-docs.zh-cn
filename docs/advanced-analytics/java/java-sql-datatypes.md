---
title: 在 SQL Server 2019 中受支持的 Java 数据类型 |Microsoft Docs
description: 将数据类型从 Java 到 SQL Server 对于输入和输出数据结构，并为 sp_execute_external_script 的输入参数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3510b53510514daa125382fc10ea33285fe44a80
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46714930"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java 和 SQL Server 支持的数据类型

这篇文章上映射到数据结构和参数的 Java 数据类型的 SQL Server 数据类型[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。

## <a name="data-types-for-data-sets"></a>数据集的数据类型

对于输入和输出数据集目前支持以下 SQL 和 Java 数据类型。

| SQL 类型        | Java 类型 | | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| smallint | ssNoversion      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | 字符串 (unicode)      | | |
| nvarchar(n) | 字符串 (unicode)      | | |
| binary(n) | byte[]      | | |
| varbinary （n) | byte[]      | | |

## <a name="data-types-for-input-parameters"></a>输入参数的数据类型

输入参数目前支持以下 SQL 和 Java 数据类型。

| SQL 类型        | Java 类型 | | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| smallint | ssNoversion      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | 字符串 (unicode)      | | |
| nvarchar(n) | 字符串 (unicode)      | | |
| binary(n) | byte[]      | | |
| varbinary （n) | byte[]      | | |
| nvarchar(max) | 字符串 (unicode)      | | |
| varbinary(max) | byte[]      | | |

## <a name="see-also"></a>另请参阅

+ [如何在 SQL Server 中调用 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 示例](java-first-sample.md)
+ [SQL Server 中的 Java 语言扩展](extension-java.md)