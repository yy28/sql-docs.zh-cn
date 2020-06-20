---
title: 升级后，新的保留关键字不能用作标识符 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- keywords [SQL Server], after upgrade
- keywords [SQL Server], reserved
- keywords [SQL Server]
ms.assetid: cb242081-54f8-4273-a8ef-52f3751c25ef
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 36f7f8cadcba5e114feee4a3c42de6f40070ce72
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045675"
---
# <a name="after-upgrade-new-reserved-keywords-cannot-be-used-as-identifiers"></a>升级后，新的保留关键字不能用作标识符
  升级顾问检测到所使用的某些词为保留关键字。 保留关键字不能用作标识符或对象名称，除非该名称用分隔符分割。  
  
## <a name="component"></a>组件  
 数据库引擎  
  
## <a name="description"></a>说明  
 在兼容级别 90 或更低级别中，以下词不是保留关键字，因此可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本中用作标识符或对象名称。 在兼容级别 100 中，以下词是完全保留的关键字，因此不应用作标识符或对象名称。  
  
-   EXTERNAL  
  
-   MERGE  
  
-   PIVOT  
  
-   REVERT  
  
-   STOPLIST  
  
-   TABLESAMPLE  
  
-   UNPIVOT  
  
## <a name="corrective-action"></a>纠正措施  
 建议您重命名该对象。 如果无法在升级前执行此操作，请使用下列方法之一，直到可以更改该名称为止：  
  
-   将数据库兼容级别设置保留为 90 或更低。  
  
-   使用分隔标识符引用对象。 例如，语句 `CREATE TABLE [MERGE] ([MERGE] int);` 使用方括号分隔对象名称合并。  
  
## <a name="external-resources"></a>外部资源  
 [保留关键字 (Transact-SQL)](/sql/t-sql/language-elements/reserved-keywords-transact-sql)  
  
 [MERGE (Transact-SQL)](/sql/t-sql/statements/merge-transact-sql)  
  
 [分隔标识符（数据库引擎）](https://go.microsoft.com/fwlink/?LinkId=112509)  
  
 [ALTER DATABASE 兼容级别 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
