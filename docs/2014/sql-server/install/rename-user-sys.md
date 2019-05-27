---
title: 重命名用户 sys |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sys user names [SQL Server]
ms.assetid: d622d646-83e4-4b6f-9a21-77b301af04b5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce8656df63c9d415ca09b54ecb86b87aba8bd83a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092863"
---
# <a name="rename-user-sys"></a>重命名 sys 用户
  升级顾问检测到的用户名称**sys**在数据库中。 该名称为保留名称。 在升级之前，请重命名该用户。 如果未重命名该用户，则数据库在升级过程结束之后将处于可疑状态并且将不可用，直至将数据库联机为止。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 用户**sys**被保留。  
  
## <a name="corrective-action"></a>纠正措施  
  
### <a name="before-upgrade-procedure"></a>升级前的步骤  
 在升级每个数据库中包含用户之前**sys**，执行以下操作：  
  
1.  创建一个新用户。  
  
2.  使用以下语句显示由用户授予的所有权限**sys** ，并向用户授予**sys**。  
  
    ```  
    -- Return permissions granted by user sys.  
    SELECT * FROM sysprotects WHERE grantor = USER_ID('sys')  
    -- Return permissions granted to user sys.  
    SELECT * FROM sysprotects WHERE uid = USER_ID('sys')  
    ```  
  
3.  将拥有的所有对象的所有权转让**sys**对新用户来说，使用**sp_changeobjectowner**。  
  
4.  删除用户**sys**。  
  
5.  若要还原在步骤 2 中捕获的原始权限，请使用 AS *new_user* GRANT 语句的子句。  
  
6.  修改脚本以引用新用户。 例如，脚本中包含的 `SELECT * FROM sys.my`_`table` 语句必须更改为 `SELECT * FROM new_user.my_table`。  
  
### <a name="after-upgrade-procedure"></a>升级后的步骤  
 如果用户**sys**已不在升级前重命名，执行以下操作：  
  
1.  执行语句`ALTER DATABASE db_name SET ONLINE`。 数据库将处于 SINGLE_USER 模式。  
  
2.  执行“升级前的步骤”部分中的所有步骤。  
  
3.  执行语句`ALTER DATABASE db_name SET MULTI_USER`。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
