---
title: "c2 audit mode 服务器配置选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], C2 Audit Mode option
- C2 auditing
- C2 Audit Mode option
- recording attempts
ms.assetid: 5a8d73a6-c4f6-4967-ba11-ecbcfc90b9cc
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 343a1670d90fbb38b8377542e7a71daafa9fd984
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="c2-audit-mode-server-configuration-option"></a>c2 审核模式服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  可以通过 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或使用 **sp_configure** 中的“c2 审核模式”选项来配置 C2 审核模式。 选择此选项将配置服务器，以记录对语句和对象的失败和成功的访问尝试。 这些信息可以帮助您了解系统活动并跟踪可能的安全策略冲突。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] C2 安全标准已经由通用准则认证所取代。 请参阅 [启用了通用准则合规性的服务器配置选项](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)。  
  
## <a name="audit-log-file"></a>审核日志文件  
 C2 审核模式数据保存在实例的默认数据目录中的某个文件内。 如果审核日志文件达到了 200 MB 的大小限制， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将创建新文件、关闭旧文件并将所有新的审核记录写入新文件。 此过程将继续下去，直到审核数据目录已满或审核被关闭。 若要确定 C2 跟踪的状态，请查询 sys.traces 目录视图。  
  
> [!IMPORTANT]  
>  C2 审核模式将大量事件信息保存在日志文件中，可能会导致日志文件迅速增大。 如果保存日志的数据目录空间不足， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将自行关闭。 如果将审核设置为自动启动，则必须使用 **-f** 标志（跳过审核）重新启动该实例或为审核日志释放更多磁盘空间。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="example"></a>示例  
 下面的示例将启用 C2 审核模式。  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
sp_configure 'c2 audit mode', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

