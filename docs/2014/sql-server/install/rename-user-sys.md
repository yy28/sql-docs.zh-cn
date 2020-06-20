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
ms.openlocfilehash: 3af9d31a54adc5645cab6fcc7104ae7ff27a61b6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059098"
---
# <a name="rename-user-sys"></a>重命名 sys 用户
  升级顾问检测到数据库中的用户名为**sys** 。 该名称为保留名称。 在升级之前，请重命名该用户。 如果未重命名该用户，则数据库在升级过程结束之后将处于可疑状态并且将不可用，直至将数据库联机为止。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 已保留用户**sys** 。  
  
## <a name="corrective-action"></a>纠正措施  
  
### <a name="before-upgrade-procedure"></a>升级前的步骤  
 升级之前，在包含用户**sys**的每个数据库中，执行以下操作：  
  
1.  创建一个新用户。  
  
2.  使用下列语句显示用户**sys**授予的所有权限，并授予用户**sys**权限。  
  
    ```  
    -- Return permissions granted by user sys.  
    SELECT * FROM sysprotects WHERE grantor = USER_ID('sys')  
    -- Return permissions granted to user sys.  
    SELECT * FROM sysprotects WHERE uid = USER_ID('sys')  
    ```  
  
3.  若要将**sys**拥有的所有对象的所有权转移给新用户，请使用**sp_changeobjectowner**。  
  
4.  删除用户**sys**。  
  
5.  若要还原在步骤2中捕获的原始权限，请使用 GRANT 语句的 AS *new_user*子句。  
  
6.  修改脚本以引用新用户。 例如，脚本中包含的 `SELECT * FROM sys.my`_`table` 语句必须更改为 `SELECT * FROM new_user.my_table`。  
  
### <a name="after-upgrade-procedure"></a>升级后的步骤  
 如果在升级之前未重命名用户**sys** ，请执行以下操作：  
  
1.  执行语句 `ALTER DATABASE db_name SET ONLINE` 。 数据库将处于 SINGLE_USER 模式。  
  
2.  执行“升级前的步骤”部分中的所有步骤。  
  
3.  执行语句 `ALTER DATABASE db_name SET MULTI_USER` 。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
