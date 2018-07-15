---
title: 创建用户定义事件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, user-defined events
- user-defined events [SQL Server]
- multiple language support [SQL Server], alerts
- languages [SQL Server], alerts
- severity levels [SQL Server]
- global considerations [SQL Server], alerts
- events [SQL Server], user-defined
- SQL Server Agent alerts, multiple-language environments
- alerts [SQL Server], user-defined events
- alerts [SQL Server], multiple-language environments
- custom events [SQL Server Agent]
- international considerations [SQL Server], alerts
ms.assetid: 03d71a35-97fa-4bba-aa9a-23ac9c9cf879
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4c59bfb6f5f2c9621d212dc52a92daecd79fad7b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313317"
---
# <a name="create-a-user-defined-event"></a>创建用户定义事件
  如果需要监视非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 预定义的事件，可以创建用户定义事件。 还可以为每个用户定义事件指定严重级别。  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 时，请为每个用户定义事件消息选择“写入 Windows 应用程序事件日志”选项，以确保记录该消息。 默认情况下，出现严重级别低于 19 的用户定义消息时，不会将其发送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 应用程序日志。 因此严重级别低于 19 的用户定义消息不会触发 SQL Server 代理警报。  
  
 用户定义事件必须具有唯一的消息号。 用户定义事件的消息号必须大于 50,000。 可以使用多种语言来定义事件的消息。 但是，在添加其他语言的错误消息之前， **En-US** 错误消息必须已经存在。  
  
 如果管理的是多语言 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境，可以使用所支持的每种语言来创建用户定义的消息。 例如，若要创建一个既用于英语服务器又用于德语服务器的新事件消息，可以在两个服务器上使用相同的消息号和严重级别，但为每个服务器指定不同的语言。  
  
 下列任务介绍了如何创建用户定义事件以及响应这些事件的警报：  
  
 **基于消息号创建警报**  
  
-   [SQL Server Management Studio](create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **基于严重级别创建警报**  
  
-   [SQL Server Management Studio](create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **定义对警报的响应**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)  
  
 **创建用户定义事件的错误消息**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql)  
  
 **修改用户定义事件的错误消息**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-altermessage-transact-sql)  
  
 **删除用户定义事件的错误消息**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-dropmessage-transact-sql)  
  
 **禁用或重新激活警报**  
  
-   [SQL Server Management Studio](disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
## <a name="see-also"></a>请参阅  
 [sp_update_alert &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
  
