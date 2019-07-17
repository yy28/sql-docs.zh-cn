---
title: DELETE-SQL 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79a9c9a86e290f568f205a7e7678122f9089a7e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096335"
---
# <a name="delete---sql-command"></a>DELETE - SQL 命令
将标记为删除的记录。  
  
 Visual FoxPro ODBC 驱动程序支持本机 Visual FoxPro 语言语法，此命令。 特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>参数  
 从 [ *DatabaseName ！* ]*TableName*  
 指定在其中记录标记为删除的表。  
  
 *DatabaseName ！* 指定如果包含数据库不是与数据源指定的数据库包含的表的数据库的名称。 必须包含的数据库，如果数据库不是与数据源指定的数据库包含的表的名称。 包含感叹号 （！） 分隔符之后的数据库名称和表名称之前。  
  
 其中*FilterCondition1*[AND&#124;或者*FilterCondition2*...]  
 指定 Visual FoxPro 将标记为删除的特定记录。  
  
 *FilterCondition*指定记录标记为删除，而必须满足的条件。 可以包含任意数量的筛选条件根据需要，将它们连接用 AND 或 OR 运算符。 此外可以使用 NOT 运算符来反转逻辑表达式的值也可以使用**空**（) 以检查是否有一个空的字段。  
  
## <a name="remarks"></a>备注  
 如果设置删除设置为 ON 时，标记为删除的记录将忽略包含作用域的所有命令。  
  
 删除-SQL 使用记录锁定时将标记为删除的表中的多个记录打开的共享访问。 这会降低在多用户的情况下记录争用，但可能会降低性能。 获得最佳性能，打开用于独占使用的表。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序将发送到数据源的 ODBC SQL 语句删除时，Visual FoxPro ODBC 驱动程序将无需转换的 Visual FoxPro 删除命令转换为该命令。  
  
## <a name="see-also"></a>请参阅  
 [SET DELETED 命令](../../odbc/microsoft/set-deleted-command.md)
