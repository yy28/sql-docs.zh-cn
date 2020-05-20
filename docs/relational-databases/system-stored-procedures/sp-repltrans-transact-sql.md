---
title: sp_repltrans （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repltrans_TSQL
- sp_repltrans
helpviewer_keywords:
- sp_repltrans
ms.assetid: 738e2322-335b-44fa-820e-f31c02743978
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9338d427a3a957a531456d9ea29448a2148b56e9
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824387"
---
# <a name="sp_repltrans-transact-sql"></a>sp_repltrans (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  返回一个结果集，它由发布数据库事务日志中所有标记为复制但没有标记为已分发的事务组成。 此存储过程在发布服务器上对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_repltrans  
```  
  
## <a name="result-sets"></a>结果集  
 **sp_repltrans**返回有关从中执行它的发布数据库的信息，使您能够查看当前未分发的事务（事务日志中尚未发送到分发服务器的事务）。 结果集显示每个事务的第一个记录和最后一个记录的日志序列号。 **sp_repltrans**类似于[&#40;transact-sql&#41;的 sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) ，但不返回事务的命令。  
  
## <a name="remarks"></a>备注  
 **sp_repltrans**用于事务复制。  
  
 非发布服务器不支持**sp_repltrans** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_repltrans**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_repldone &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
