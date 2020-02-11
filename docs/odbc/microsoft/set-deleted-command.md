---
title: SET DELETED 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54900f00e03e1f236baf0b6eef152081b1f384a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997733"
---
# <a name="set-deleted-command"></a>SET DELETED 命令
指定是否处理标记为删除的记录以及是否可在其他命令中使用这些记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （驱动程序的默认值; Visual FoxPro 的默认值为 OFF。）指定使用作用域对记录（包括相关表中的记录）执行的命令将忽略标记为删除的记录。  
  
 OFF  
 指定可以通过使用作用域对记录执行的命令（包括相关表中的记录）来访问标记为删除的记录。  
  
## <a name="remarks"></a>备注  
 如果对表进行索引（）时，使用已删除的（）测试记录状态的查询可以使用 Visual FoxPro 雕像技术进行优化。  
  
> [!IMPORTANT]  
>  如果命令的默认作用域是当前记录或包括单个记录的作用域，则将忽略 SET DELETED。 INDEX 始终忽略 SET DELETED，并为表中的所有记录编制索引。  
  
## <a name="see-also"></a>另请参阅  
 [DELETE - SQL 命令](../../odbc/microsoft/delete-sql-command.md)
