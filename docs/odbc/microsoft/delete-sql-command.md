---
title: 删除 - SQL 命令 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9757fd57d999815964266c035963de1129eaf5e8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303548"
---
# <a name="delete---sql-command"></a>DELETE - SQL 命令
标记记录以进行删除。  
  
 Visual FoxPro ODBC 驱动程序支持此命令的本机 Visual FoxPro 语言语法。 有关特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>参数  
 从 [*数据库名称！*]*表名称*  
 指定在其中标记记录以进行删除的表。  
  
 *数据库名称！* 指定包含表的数据库的名称，如果包含的数据库不是使用数据源指定的数据库。 如果数据库不是使用数据源指定的数据库，则必须包含包含表的数据库的名称。 包括数据库名称后和表名称之前的感叹号 （！） 分隔符。  
  
 其中*筛选条件1*[和&#124;或*过滤器条件2*...]  
 指定 Visual FoxPro 仅标记某些记录以进行删除。  
  
 *筛选器条件*指定记录必须满足的条件才能标记为删除。 您可以根据需要包含尽可能多的筛选器条件，将它们与 AND 或 OR 运算符连接。 您还可以使用 NOT 运算符反转逻辑表达式的值，也可以使用**EMPTY**（ ） 检查空字段。  
  
## <a name="remarks"></a>备注  
 如果 SET DELETED 设置为"打开"，则标记为删除的记录将被包含作用域的所有命令忽略。  
  
 删除 - SQL 在标记多个记录以在打开的用于共享访问的表中删除时使用记录锁定。 这减少了多用户情况下的记录争用，但会降低性能。 为了达到最佳性能，打开表以专供独占使用。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当您的应用程序将 ODBC SQL 语句 DELETE 发送到数据源时，Visual FoxPro ODBC 驱动程序将该命令转换为 Visual FoxPro DELETE 命令，无需翻译。  
  
## <a name="see-also"></a>另请参阅  
 [SET DELETED 命令](../../odbc/microsoft/set-deleted-command.md)
