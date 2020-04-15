---
title: 设置删除命令 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b3302dc7eecca7135dab9dff5afa376169be0f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300877"
---
# <a name="set-deleted-command"></a>SET DELETED 命令
指定是否处理标记为删除的记录以及这些记录是否可用于其他命令。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （驱动程序的默认值;Visual FoxPro 的默认值为 OFF。指定使用作用域对记录（包括相关表中的记录）运行的命令忽略标记为要删除的记录。  
  
 OFF  
 指定标记为删除的记录可以通过使用作用域对记录（包括相关表中的记录）操作的命令进行访问。  
  
## <a name="remarks"></a>备注  
 如果使用 DELETED（ ） 测试记录状态的查询，如果表在 DELETED（） 上编制索引，则可以使用 Visual FoxPro Rushmore 技术进行优化。  
  
> [!IMPORTANT]  
>  如果命令的默认范围是当前记录，或者包含单个记录的范围，则忽略 SET DELETED。 INDEX 始终忽略"设置删除"并索引表中的所有记录。  
  
## <a name="see-also"></a>另请参阅  
 [DELETE - SQL 命令](../../odbc/microsoft/delete-sql-command.md)
