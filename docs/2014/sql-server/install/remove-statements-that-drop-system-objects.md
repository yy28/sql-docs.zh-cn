---
title: 删除用于删除系统对象的语句 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4c017e6fedbc7fd994e5b2d2ca4de184a082da65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015831"
---
# <a name="remove-statements-that-drop-system-objects"></a>删除用于去除系统对象的语句
  升级顾问检测到用于删除系统对象的语句。 系统对象，包括扩展存储的过程，都将以只读方式部署**资源**数据库 (mssqlsystemresource)，无法删除。 请修改您的应用程序以撤消或拒绝针对系统对象的 EXECUTE 权限。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 DROP TABLE，DROP PROCEDURE 等语句和**sp_dropextendedproc**无法用于删除系统对象，因为这些对象都将以只读方式部署**资源**数据库。  
  
## <a name="corrective-action"></a>纠正措施  
 从您的应用程序中删除所有试图删除系统对象的语句。 请修改您的应用程序以撤消或拒绝针对系统对象的 EXECUTE 权限。 另外，也可以使用外围应用配置器 (SAC) 工具禁用这些对象中的部分对象。 例如， **xp_cmdshell**扩展存储的过程可以禁用或启用使用 SAC 工具。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
