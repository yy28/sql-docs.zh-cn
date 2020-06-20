---
title: 将用户定义数据库的排序规则设置为与 master 和 model 数据库的排序规则 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c686446f-dae1-4b05-a3df-837b3422988d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b48696fb56c40062d62f04845715170887f84fda
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929148"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-those-of-the-master-and-model-databases"></a>将用户定义的数据库排序规则设置为与 master 和 model 数据库的排序规则一致
  此规则检查用户定义的数据库是否是使用与 master 或 model 相同的数据库排序规则进行定义的。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 建议用户定义的数据库排序规则与 master 或 model 的排序规则一致。 否则，可能会发生使代码无法执行的排序规则冲突。 例如，当存储过程将一个表连接到一个临时表时，如果用户定义的数据库排序规则与 model 数据库的排序规则不同，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可能会结束该批处理并返回一个排序规则冲突错误。 出现这种情况的原因是临时表是在 tempdb 中创建的，而后者的排序规则基于 model 的排序规则。  
  
 如果遇到排序规则冲突错误，请考虑下面的解决方案之一：  
  
-   从用户数据库中导出数据，并将该数据导入排序规则与 master 和 model 数据库排序规则相同的新表中。  
  
-   重新生成系统数据库以使用与用户数据库排序规则一致的排序规则。 有关如何重新生成系统数据库的详细信息，请参阅[重新生成系统数据库](../relational-databases/databases/system-databases.md)。  
  
-   修改将用户表连接到 tempdb 中的表的任何存储过程，以便使用用户数据库的排序规则在 tempdb 中创建表。 为此，请在临时表的列定义中添加 `COLLATE database_default` 子句，如下面的示例所示：  
  
    ```  
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )  
    ```  
  
## <a name="for-more-information"></a>有关详细信息  
 [设置或更改数据库排序规则](../relational-databases/collations/set-or-change-the-database-collation.md)  
  
 [设置或更改列排序规则](../relational-databases/collations/set-or-change-the-column-collation.md)  
  
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [COLLATE (Transact-SQL)](/sql/t-sql/statements/collations)  
  
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [Microsoft 知识库文章325335](https://go.microsoft.com/fwlink/?linkid=117751)  
  
 [如何从命令提示符安装 SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=81585)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳做法](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
