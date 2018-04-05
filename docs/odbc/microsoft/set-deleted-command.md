---
title: 设置已删除命令 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 50364dfbbebb7b16b1438e3e17e0e1bbabc30cef
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="set-deleted-command"></a>设置已删除命令
指定是否已处理标记为删除的记录，并指明它们是否可在其他命令中使用。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （默认为驱动程序; Visual FoxPro 的默认值为 OFF。）指定的命令运行 （包括相关表中的记录） 的记录所使用范围忽略标记为删除的记录。  
  
 OFF  
 指定记录标记为删除可以访问由记录 （包括相关表中的记录） 运行的命令使用范围。  
  
## <a name="remarks"></a>Remarks  
 查询可以使用 Visual FoxPro Rushmore 技术，如果表索引上已删除 （） 优化使用已删除 （） 若要测试的记录的状态。  
  
> [!IMPORTANT]  
>  该命令的默认作用域是当前记录是否包括单个记录的作用域，则设置删除将被忽略。 索引始终忽略设置删除和索引表中的所有记录。  
  
## <a name="see-also"></a>另请参阅  
 [DELETE - SQL 命令](../../odbc/microsoft/delete-sql-command.md)
