---
title: 删除用于去除系统对象的语句 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68e5000e924c438a4611e2fa8c134f0dd822f930
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59581541"
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
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
