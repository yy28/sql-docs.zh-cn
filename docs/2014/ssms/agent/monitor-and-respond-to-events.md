---
title: 监视事件和响应事件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- notifications [SQL Server], alert
- events [SQL Server], alerts
- alerts [SQL Server]
- notifications [SQL Server]
- events [SQL Server], automatically responding to
- administrator notifications [SQL Server Agent]
- automatic event responses
- SQL Server Agent alerts
- monitoring [SQL Server], events
- responding to events automatically
ms.assetid: f7fbe155-5b68-4777-bc71-a47637471f32
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 18dce0f5566da3cae4de2f0943ac32fc93a1fc94
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189714"
---
# <a name="monitor-and-respond-to-events"></a>监视事件和响应事件
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理可监视并自动响应*事件*，例如来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的消息、特定性能条件以及 Windows Management Instrumentation (WMI) 事件。  
  
## <a name="in-this-section"></a>本节内容  
 [警报](alerts.md)  
 介绍了命名警报以及选择警报响应的事件或性能条件。  
  
 [创建用户定义事件](create-a-user-defined-event.md)  
 介绍了如何创建由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]预定义的事件以外的事件。  
  
 [运算符](operators.md)  
 介绍了为管理员创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理可用于在作业失败或成功时用来发送通知的别名。  
  
## <a name="about-monitoring-and-responding-to-events"></a>关于监视事件和响应事件  
 对事件的自动响应称为“警报”。 您可以针对一个或多个事件定义警报，指定希望 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理如何响应发生的这些事件。 警报可以通过通知管理员和/或运行某项作业来响应事件。 警报还可以将事件转发到其他计算机上的 Microsoft Windows 应用程序日志。 例如，您可以指定在发生严重性为 19 的事件时立即通知操作员。 通过定义警报，数据库管理员可以更有效地监视和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理只响应定义了警报的事件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理用来监视事件的方法取决于事件的类型。  
  
 当为一个性能计数器定义了一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理警报后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将直接监视该性能计数器。 对于 WMI 事件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理为 WMI 事件注册一个事件查询。  
  
 为了响应来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的消息， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理会监视 Windows 应用程序日志。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理只能响应此日志中出现的消息。 默认情况下，SQL Server 将下列消息记录在 Windows 应用程序日志中：  
  
-   严重性为 19 或更高的 sysmessages 错误。  
  
     如果您还希望记录严重性低于 19 的特定 sysmessages 错误，请使用 sp_altermessage 存储过程将这类错误指定为“始终记录”。  
  
-   所有使用 WITH LOG 语法调用的 RAISERROR 语句。  
  
     建议使用 RAISERROR WITH LOG 将 SQL Server 实例的相关信息写入 Windows 应用程序日志。  
  
-   所有使用 xp_logevent 记录的应用程序事件。  
  
    > [!NOTE]  
    >  记录应用程序事件会占用日志空间，并导致 Windows 应用程序日志超出其最大大小。 请确保 Windows 应用程序日志最大大小足够大，以免丢失 SQL Server 事件信息。  
  
 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 记录消息时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务将该消息与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员定义的警报进行比较。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务通过执行事件警报中指定的任务来响应事件，而不管事件的源是什么。  
  
## <a name="see-also"></a>请参阅  
 [sp_altermessage &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-altermessage-transact-sql)  
  
  
