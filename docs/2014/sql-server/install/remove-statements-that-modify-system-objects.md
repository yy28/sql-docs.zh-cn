---
title: 删除修改系统对象的语句 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- direct system catalog updates [SQL Server]
- system catalogs [SQL Server]
ms.assetid: 221b46c2-c27e-4df8-bd8c-8b990d6d5e98
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 526181bc4bf7ab81df2eaa25f19e7627c9b7af10
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059154"
---
# <a name="remove-statements-that-modify-system-objects"></a>删除用于修改系统对象的语句
  升级顾问检测到了用于更新系统目录的语句。 不允许直接更新系统目录。 请修改您的 SQL 脚本，使用正式且有记录的 API。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 不允许直接更新系统目录。 尝试这样做将生成以下错误：  
  
 `Server: Msg 259, Level 16, State 1, Line 1`  
  
 `Ad hoc updates to system catalogs are not allowed.`  
  
## <a name="corrective-action"></a>纠正措施  
 请修改您的 SQL 脚本，使用正式且有记录的 API。 例如，使用 ALTER DATABASE *database_name*设置紧急情况，而不是对**sysdatabases**系统表运行 UPDATE 语句。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
