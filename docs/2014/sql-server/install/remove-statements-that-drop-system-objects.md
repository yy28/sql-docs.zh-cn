---
title: 删除删除系统对象的语句 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d420e2dba1dfdb284b0002eca6d8408c4e019e8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093079"
---
# <a name="remove-statements-that-drop-system-objects"></a>删除用于去除系统对象的语句
  升级顾问检测到用于删除系统对象的语句。 系统对象（包括扩展存储过程）部署在只读**资源**数据库（mssqlsystemresource.mdf）中，不能删除。 请修改您的应用程序以撤消或拒绝针对系统对象的 EXECUTE 权限。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 不能使用 DROP TABLE、DROP PROCEDURE 和**sp_dropextendedproc**等语句删除系统对象，因为这些对象部署在只读**资源**数据库中。  
  
## <a name="corrective-action"></a>纠正措施  
 从您的应用程序中删除所有试图删除系统对象的语句。 请修改您的应用程序以撤消或拒绝针对系统对象的 EXECUTE 权限。 另外，也可以使用外围应用配置器 (SAC) 工具禁用这些对象中的部分对象。 例如，可以使用 SAC 工具禁用或启用**xp_cmdshell**扩展存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
