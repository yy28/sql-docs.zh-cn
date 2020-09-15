---
title: 将用户定义数据库的排序规则设置为与 master 和模型数据库一致
description: 了解如何启用策略来检查用户定义数据库的排序规则是否与系统数据库的排序规则相同。
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 905accc62afdc12152110d44a18e61d4c8a9bcef
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284866"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-master-and-model-databases"></a>将用户定义数据库的排序规则设置为与 master 和模型数据库一致
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此规则检查用户定义的数据库是否是使用与 master 或 model 相同的数据库排序规则进行定义的。
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 建议用户定义的数据库排序规则与 master 或 model 的排序规则一致。 否则，可能会发生使代码无法执行的排序规则冲突。 例如，当存储过程将一个表联接到一个临时表时，如果用户定义数据库的排序规则与模型数据库不同，SQL Server 可能会结束该批处理并返回一个排序规则冲突错误。 出现这种情况的原因是临时表是在 tempdb 中创建的，而后者的排序规则基于 model 的排序规则。

  如果遇到排序规则冲突错误，请考虑下面的解决方案之一：

  - 从用户数据库中导出数据，并将该数据导入排序规则与 master 和 model 数据库排序规则相同的新表中。

  - 重新生成系统数据库以使用与用户数据库排序规则一致的排序规则。 有关如何重新生成系统数据库的详细信息，请参阅[重新生成系统数据库](../databases/rebuild-system-databases.md)。

  - 修改将用户表连接到 tempdb 中的表的任何存储过程，以便使用用户数据库的排序规则在 tempdb 中创建表。 为此，请在临时表的列定义中添加 COLLATE database_default 子句，如下面的示例所示：
  
    ```
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )
    ```

## <a name="see-also"></a>另请参阅
  
 [设置或更改服务器排序规则](../collations/set-or-change-the-server-collation.md)  

 [设置或更改数据库排序规则](../collations/set-or-change-the-database-collation.md)

 [设置或更改列排序规则](../collations/set-or-change-the-column-collation.md)
 
 [查看排序规则信息](../collations/view-collation-information.md)    
  
  
