---
title: sp_replication_agent_checkup (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_replication_agent_checkup_TSQL
- sp_replication_agent_checkup
helpviewer_keywords:
- sp_replication_agent_checkup
ms.assetid: 50357c2e-71aa-4e13-9e2e-0977a3655cc9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e47b20344f9fc636445d0c322c0736b7aea1d7b4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603586"
---
# <a name="spreplicationagentcheckup-transact-sql"></a>sp_replication_agent_checkup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  检查每个分发数据库的复制代理，这些代理正在运行但在指定检测信号间隔内没有历史记录。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@heartbeat_interval** =] **'***heartbeat_interval*****  
 是的最大代理可以运行而无需记录进度消息的分钟数。 *heartbeat_interval*是**int**，默认值为 10 分钟。  
  
## <a name="return-code-values"></a>返回代码值  
 **sp_replication_agent_checkup**为检测为可疑到每个代理引发 14151 号错误。 它还记录关于这些代理的失败历史记录消息。  
  
## <a name="remarks"></a>备注  
 **sp_replication_agent_checkup**快照复制、 事务复制和合并复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_replication_agent_checkup**。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
