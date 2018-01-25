---
title: "检查点 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKPOINT_TSQL
- CHECKPOINT
dev_langs: TSQL
helpviewer_keywords:
- events [SQL Server], checkpoints
- automatic checkpoints
- writing dirty pages to disk
- pages [SQL Server], dirty
- checkpoints [SQL Server]
- CHECKPOINT statement
- log truncate mode [SQL Server]
- dirty pages
- logs [SQL Server], checkpoints
- manual checkpoints [SQL Server]
- pages [SQL Server], checkpoints
ms.assetid: ccdfc689-ad4e-44c0-83f7-0f2cfcfb6406
caps.latest.revision: "59"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6353bd534827ff9066bd7b184a09d67b5867c3cb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="checkpoint-transact-sql"></a>CHECKPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在您当前连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中生成一个手动检查点。  
  
> [!NOTE]  
>  有关不同类型的数据库检查点和在常规的检查点操作的信息，请参阅[数据库检查点 &#40;SQL server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CHECKPOINT [ checkpoint_duration ]  
```  
  
## <a name="arguments"></a>参数  
 *checkpoint_duration*  
 以秒为单位指定手动检查点完成所需的时间。 当*checkpoint_duration*指定，则[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]尝试执行的请求的持续时间内的检查点。 *Checkpoint_duration*必须是类型的表达式**int**并且必须是大于零。 如果省略该参数，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将调整检查点持续时间，以便最大程度地降低对数据库应用程序性能的影响。 *checkpoint_duration*是一个高级的选项。  
  
## <a name="factors-affecting-the-duration-of-checkpoint-operations"></a>影响检查点操作持续时间的因素  
 通常，执行检查点操作所需的时间会随着该操作必须写入的脏页数的增加而增加。 默认情况下，为最大程度地降低对其他应用程序性能的影响，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将调整检查点操作执行写入的频率。 降低写频率将增加完成检查点操作所需的时间。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用此策略对手动检查点，除非*checkpoint_duration*检查点命令中指定值。  
  
 使用的性能影响*checkpoint_duration*取决于若干脏页、 系统和指定的实际持续时间上的活动。 例如，如果检查点通常将在 120 秒内完成的则指定*checkpoint_duration* 45 秒原因的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以更多资源投入到不是将默认情况下分配的检查点。 与此相反，指定*checkpoint_duration*的 180 秒的时间可能会导致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将分配较少的资源不是将默认分配。 通常，一个短*checkpoint_duration*时 long 类型的值将增加资源，专用于检查点， *checkpoint_duration*将减少专用于检查点的资源。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 总是尽可能地完成检查点操作，并且操作完成后，CHECKPOINT 语句将立即返回。 因此，完成检查点的时间有时比指定的持续时间短，有时则比指定的持续时间长。  
  
##  <a name="Security"></a> 安全性  
  
### <a name="permissions"></a>权限  
 检查点权限仅默认授予的成员**sysadmin**固定的服务器角色和**db_owner**和**db_backupoperator**固定数据库角色的成员，并不是转让。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [数据库检查点 (SQL Server)](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [配置恢复间隔服务器配置选项](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)  
  
  
