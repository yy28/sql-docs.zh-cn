---
title: Sp_helptrigger 输出中的新列可能会影响应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- sp_helptrigger
ms.assetid: b7c42a8f-f2e0-4fa3-b046-3cf39c854c47
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c7ad878072f8139cc95d6dc34c01f5f48835774a
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59581654"
---
# <a name="new-column-in-output-of-sphelptrigger-may-impact-applications"></a>sp_helptrigger 输出中的新列可能会影响应用程序
  trigger_schemaias 结果集中的最后一列返回的 sp_helptrigger 系统存储过程。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]若要获取有关针对特定表定义的触发器的信息，请查询 sys.triggers目录视图。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 检查应用程序中是否使用了 sp_helptrigger。 可能需要修改应用程序以容纳附加列。 另外，还可以改用 sys.triggers 目录视图。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
