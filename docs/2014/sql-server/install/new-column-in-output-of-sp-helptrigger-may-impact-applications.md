---
title: Sp_helptrigger 的输出中的新列可能会影响应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sp_helptrigger
ms.assetid: b7c42a8f-f2e0-4fa3-b046-3cf39c854c47
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 33d47c858a03766260e8ed8c098fef79e9e4a82f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093741"
---
# <a name="new-column-in-output-of-sp_helptrigger-may-impact-applications"></a>sp_helptrigger 输出中的新列可能会影响应用程序
  trigger_schemaias sp_helptrigger 系统存储过程返回的结果集中的最后一列。  
  
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]若要获取有关针对特定表定义的触发器的信息，请查询 sys.triggers目录视图。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 检查应用程序中是否使用了 sp_helptrigger。 可能需要修改应用程序以容纳附加列。 另外，还可以改用 sys.triggers 目录视图。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
