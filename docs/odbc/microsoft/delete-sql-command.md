---
title: "删除的 SQL 命令 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8effde0f80a219f11af460bdc941a9b6d9681455
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="delete---sql-command"></a>删除的 SQL 命令
将标记为删除的记录。  
  
 Visual FoxPro ODBC 驱动程序支持本机 Visual FoxPro 语言语法，此命令。 特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>参数  
 从 [ *DatabaseName ！*]*TableName*  
 指定在其中记录已标记为删除的表。  
  
 *DatabaseName ！* 指定如果包含数据库不是指定与数据源的数据库包含的表的数据库的名称。 必须包括包含的表，如果数据库不是指定与数据源的数据库的数据库的名称。 之后的数据库名称和表名称之前，请包括感叹号 （！） 分隔符。  
  
 其中*FilterCondition1*[AND &#124;或者*FilterCondition2*...]  
 指定 Visual FoxPro 将标记为删除的特定记录。  
  
 *FilterCondition*指定记录标记为要删除所必须满足的条件。 可以包含任意数量的筛选条件所需将它们连接使用 AND 或 OR 运算符。 你还可以使用 NOT 运算符颠倒的逻辑表达式时，值或可以使用**空**（) 检查是否有一个空的字段。  
  
## <a name="remarks"></a>注释  
 如果设置删除设置为 ON，标记为删除的记录将忽略由包含作用域的所有命令。  
  
 删除-SQL 使用记录锁定时将标记为删除表中的多个记录打开以进行共享访问。 这将减少在多用户情况下记录争用，但会降低性能。 为获得最佳性能，打开以供独占使用的表。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序将 ODBC SQL 语句删除发送到数据源时，Visual FoxPro ODBC 驱动程序将不转换 Visual FoxPro DELETE 命令转换为命令。  
  
## <a name="see-also"></a>另请参阅  
 [设置已删除命令](../../odbc/microsoft/set-deleted-command.md)

