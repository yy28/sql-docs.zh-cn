---
title: 启用查询通知
description: 介绍如何使用查询通知（包括启用和使用查询通知的要求）。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 94b472a1fe040aa3a684d9f7b523ba09c82a651e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452234"
---
# <a name="enabling-query-notifications"></a>启用查询通知

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

使用查询通知的应用程序有一组通用的要求。 必须正确配置数据源才能支持 SQL 查询通知，并且用户必须具有正确的客户端和服务器端权限。  
  
若要使用查询通知，你必须：  
  
- 启用数据库的查询通知。  
  
- 确保用于连接到数据库的用户 ID 具有所需的权限。  
  
- 使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象通过关联的通知对象（<xref:Microsoft.Data.SqlClient.SqlDependency> 或 <xref:Microsoft.Data.Sql.SqlNotificationRequest>）执行有效的 SELECT 语句。  
  
- 如果被监视的数据发生更改，请提供处理通知的代码。  
  
## <a name="query-notifications-requirements"></a>查询通知要求  
仅满足特定要求的 SELECT 语句支持查询通知。 下表提供了指向 SQL Server 联机丛书中 Service Broker 和查询通知文档的链接。  
  
**SQL Server 文档**  
  
- [为通知创建查询](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Service Broker 的安全注意事项](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [安全性和保护 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Notification Services 的安全注意事项](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [查询通知权限](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Service Broker 的国际化注意事项](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [解决方案设计注意事项 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Service Broker 开发人员信息中心](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [开发人员指南 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>启用查询通知以运行示例代码  
若要通过使用 SQL Server Management Studio 在 AdventureWorks 数据库上启用 Service Broker，请执行下面的 Transact-SQL 语句：  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
要使查询通知示例正常运行，必须在数据库服务器上执行以下 Transact-sql 语句。  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>查询通知权限  
执行请求通知的命令的用户必须具有对服务器的 "订阅查询通知" 数据库权限。  
  
在部分信任情况下运行的客户端代码需要 <xref:Microsoft.Data.SqlClient.SqlClientPermission>。  
  
下面的代码创建一个 <xref:Microsoft.Data.SqlClient.SqlClientPermission> 对象，并将 <xref:System.Security.Permissions.PermissionState> 设置为 <xref:System.Security.Permissions.PermissionState.Unrestricted>。 如果调用堆栈中的所有高级调用方未被授予权限，<xref:System.Security.CodeAccessPermission.Demand%2A> 将在运行时强制执行 <xref:System.Security.SecurityException>。  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>选择通知对象  
查询通知 API 提供两个用于处理通知的对象：<xref:Microsoft.Data.SqlClient.SqlDependency> 和 <xref:Microsoft.Data.Sql.SqlNotificationRequest>。
  
### <a name="using-sqldependency"></a>使用 SqlDependency  
要使用 <xref:Microsoft.Data.SqlClient.SqlDependency>，必须对所使用的 SQL Server 数据库启用 Service Broker，并且用户必须具有接收通知的权限。 Service Broker 对象（如通知队列）已预定义。  
  
此外，在将通知发布到队列中时，<xref:Microsoft.Data.SqlClient.SqlDependency> 会自动启动辅助线程来处理通知;它还分析 Service Broker 消息，将信息公开为事件参数数据。 <xref:Microsoft.Data.SqlClient.SqlDependency> 必须通过调用 `Start` 方法进行初始化，以建立与数据库的依赖关系。 这是一个静态方法，只需在应用程序初始化期间为每个所需的数据库连接调用一次。 必须在应用程序终止时为执行的每个相关连接调用 `Stop` 方法。  
  
### <a name="using-sqlnotificationrequest"></a>使用 SqlNotificationRequest  
与此相反，<xref:Microsoft.Data.Sql.SqlNotificationRequest> 要求您自己实现整个侦听基础结构。 此外，必须定义队列所支持的所有支持 Service Broker 对象，例如队列、服务和消息类型。 如果你的应用程序需要特殊通知消息或通知行为，或如果你的应用程序是更大的 Service Broker 应用程序的一部分，则此手动方法非常有用。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 中的查询通知](query-notifications-sql-server.md)
