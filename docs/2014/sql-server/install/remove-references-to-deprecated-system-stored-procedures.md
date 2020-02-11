---
title: 删除对不推荐使用的系统存储过程的引用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- undocumented system stored procedures [SQL Server]
- system stored procedures [SQL Server]
ms.assetid: 487d24fc-41d5-495e-843c-0ac974ec472f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2e841956adf08f9ac14a3f1360839e9132bf9cd6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093106"
---
# <a name="remove-references-to-deprecated-system-stored-procedures"></a>删除对不推荐使用的系统存储过程的引用
  升级顾问检测到一些语句引用了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不再可用的未记录的系统存储过程和扩展存储过程。 引用这些对象的语句将失败。 请勿使用未记录的系统对象或 API，因为在将来的版本中该功能可能会更改或删除，且不会给出相关通知。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
  
### <a name="documented-system-stored-procedures"></a>已记录的系统存储过程  
 以下已记录的系统存储过程已被删除：  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
### <a name="undocumented-system-stored-procedures"></a>未记录的系统存储过程  
 以下未记录的系统存储过程和扩展存储过程已被删除：  
  
-   sp_articlesynctranprocs  
  
-   sp_diskdefault  
  
-   sp_EventLog  
  
-   sp_GetMBCSCharLen  
  
-   sp_helplog  
  
-   sp_helpsql  
  
-   sp_IsMBCSLeadByte  
  
-   sp_lock2  
  
-   sp_MSget_current_activity  
  
-   sp_MSset_current_activity  
  
-   sp_MSobjessearch  
  
-   xp_enum_ActiveScriptEngines  
  
-   xp_eventlog  
  
-   xp_GetAdminGroupName  
  
-   xp_GetFileDetails  
  
-   xp_GetLocalSystemAccountName  
  
-   xp_IsNTAdmin  
  
-   xp_MSLocalSystem  
  
-   xp_MSnt2000  
  
-   xp_MSplatform  
  
-   xp_SetSecurity  
  
-   xp_varbintohexstr  
  
## <a name="corrective-action"></a>纠正措施  
  
### <a name="documented-system-stored-procedures"></a>已记录的系统存储过程  
 按照下表修改应用程序。  
  
|不再使用|操作|  
|----------------|-------------|  
|sp_addalias|请将别名替换为用户帐户和数据库角色的组合。 有关详细信息，请参阅 SQL Server 联机丛书中的“CREATE USER (Transact-SQL)”和“CREATE ROLE (Transact-SQL)”。 使用 sp_dropalias 删除已升级数据库中的别名。|  
|sp_addgroupsp_changegroup<br /><br /> sp_dropgroup<br /><br /> sp_helpgroup|使用角色。 有关详细信息，请参阅 SQL Server 联机丛书中的“服务器级别角色”和“数据库级别角色”。|  
  
### <a name="undocmented-system-stored-procedures"></a>Undocmented 系统存储过程  
 可创建具有等效功能的 CLR 存储过程来替换未记录的系统存储过程。 有关详细信息，请参阅 SQL Server 联机丛书中的“CLR 存储过程”。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
