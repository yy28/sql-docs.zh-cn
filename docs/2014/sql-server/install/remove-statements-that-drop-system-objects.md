---
title: 删除用于去除系统对象的语句 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
caps.latest.revision: 18
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7bb577db82aae98356481657faa9bd76a0ab2a82
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161828"
---
# <a name="remove-statements-that-drop-system-objects"></a>删除用于去除系统对象的语句
  升级顾问检测到用于删除系统对象的语句。 系统对象，包括扩展存储的过程，部署在只读**资源**数据库 (mssqlsystemresource) 中，不能删除。 请修改您的应用程序以撤消或拒绝针对系统对象的 EXECUTE 权限。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 诸如 DROP TABLE、 DROP PROCEDURE 语句和**sp_dropextendedproc**不能用于删除系统对象，因为这些对象部署在只读**资源**数据库。  
  
## <a name="corrective-action"></a>纠正措施  
 从您的应用程序中删除所有试图删除系统对象的语句。 请修改您的应用程序以撤消或拒绝针对系统对象的 EXECUTE 权限。 另外，也可以使用外围应用配置器 (SAC) 工具禁用这些对象中的部分对象。 例如， **xp_cmdshell**扩展存储的过程可以禁用或启用使用 SAC 工具。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
