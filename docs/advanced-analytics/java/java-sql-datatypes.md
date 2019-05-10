---
title: 在 SQL Server 2019-SQL Server 语言扩展中受支持的 Java 数据类型
description: 将数据类型从 Java 到 SQL Server 对于输入和输出数据结构，并为 sp_execute_external_script 的输入参数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 14a2bc5594b16610dfb8278ab82a9e7b8b22fea6
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774999"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java 和 SQL Server 支持的数据类型

这篇文章上映射到数据结构和参数的 Java 数据类型的 SQL Server 数据类型[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。

## <a name="data-types-for-data-sets"></a>数据集的数据类型

对于输入和输出数据集目前支持以下 SQL 和 Java 数据类型。


| SQL 数据类型        | Java 数据类型 | 注释 | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| smallint | ssNoversion      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | String      | | |
| nvarchar(n) | String      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | String      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | String | | |
| char(n) | String | 仅支持 UTF8 字符串 | |
| varchar(n) | String | 仅支持 UTF8 字符串 | |
| varchar(max) | String | 仅支持 UTF8 字符串 | |

## <a name="data-types-for-input-parameters"></a>输入参数的数据类型

输入参数目前支持以下 SQL 和 Java 数据类型。

| SQL 数据类型        | Java 数据类型 | 注释 | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| smallint | ssNoversion      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | String      | | |
| nvarchar(n) | String      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | String      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | String | | |
| char(n) | String | 仅支持 UTF8 字符串 | |
| varchar(n) | String | 仅支持 UTF8 字符串 | |
| varchar(max) | String | 仅支持 UTF8 字符串 | |

## <a name="next-steps"></a>后续步骤

+ [如何在 SQL Server 中调用 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 示例](java-first-sample.md)
+ [SQL Server 中的 Java 语言扩展](extension-java.md)
