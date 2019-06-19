---
title: 创建用户定义事件 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
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
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f4b13211edd8d22116607dda97f792e2d362d522
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65095507"
---
# <a name="create-a-user-defined-event"></a>创建用户定义事件
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

如果需要监视非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 预定义的事件，可以创建用户定义事件。 还可以为每个用户定义事件指定严重级别。  
  
> [!NOTE]  
> 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 时，请为每个用户定义事件消息选择“写入 Windows 应用程序事件日志”  选项，以确保记录该消息。 默认情况下，出现严重级别低于 19 的用户定义消息时，不会将其发送到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 应用程序日志。 因此严重级别低于 19 的用户定义消息不会触发 SQL Server 代理警报。  
  
用户定义事件必须具有唯一的消息号。 用户定义事件的消息号必须大于 50,000。 可以使用多种语言来定义事件的消息。 但是，在添加其他语言的错误消息之前， **En-US** 错误消息必须已经存在。  
  
如果管理的是多语言 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境，可以使用所支持的每种语言来创建用户定义的消息。 例如，若要创建一个既用于英语服务器又用于德语服务器的新事件消息，可以在两个服务器上使用相同的消息号和严重级别，但为每个服务器指定不同的语言。  
  
下列任务介绍了如何创建用户定义事件以及响应这些事件的警报：  
  
**基于消息号创建警报**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**基于严重级别创建警报**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**定义对警报的响应**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)  
  
**创建用户定义事件的错误消息**  
  
-   [Transact-SQL](https://msdn.microsoft.com/54746d30-f944-40e5-a707-f2d9be0fb9eb)  
  
**修改用户定义事件的错误消息**  
  
-   [Transact-SQL](https://msdn.microsoft.com/1b28f280-8ef9-48e9-bd99-ec14d79abaca)  
  
**删除用户定义事件的错误消息**  
  
-   [Transact-SQL](https://msdn.microsoft.com/17287a15-cdde-43d1-bb18-9f920bc15db8)  
  
**禁用或重新激活警报**  
  
-   [SQL Server Management Studio](../../ssms/agent/disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  
## <a name="see-also"></a>另请参阅  
[sp_update_alert (Transact-SQL)](https://msdn.microsoft.com/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  
