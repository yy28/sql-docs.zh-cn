---
title: 启用查询通知
description: 介绍如何使用查询通知，其中包括启用和使用查询通知的要求。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 1fae73102dbbb29b6772213c4d021c273271458a
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725629"
---
# <a name="enabling-query-notifications"></a>启用查询通知

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

使用查询通知的应用程序具有一组通用的要求。 必须正确配置数据源才能支持 SQL 查询通知，并且用户必须具有正确的客户端和服务器端权限。  
  
若要使用查询通知，必须：  
  
- 为数据库启用查询通知。  
  
- 确保用于连接数据库的用户 ID 具有所需的权限。  
  
- 使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象与关联的通知对象（<xref:Microsoft.Data.SqlClient.SqlDependency> 或 <xref:Microsoft.Data.Sql.SqlNotificationRequest>）一起执行有效的 SELECT 语句。  
  
- 如果要监视的数据发生更改，请提供代码以处理通知。  
  
## <a name="query-notifications-requirements"></a>查询通知要求  
只有满足下列特定要求的 SELECT 语句才支持查询通知。 下表提供了指向 SQL Server 联机丛书中的 Service Broker 和查询通知文档的链接。  
  
**SQL Server 文档**  
  
- [为通知创建查询](/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Service Broker 的安全注意事项](/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [安全性和保护 (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Notification Services 的安全注意事项](/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [查询通知权限](/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Service Broker 的国际化注意事项](/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [解决方案设计注意事项 (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Service Broker 开发人员信息中心](/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [开发人员指南 (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>启用查询通知以运行示例代码  
若要通过使用 SQL Server Management Studio 在 AdventureWorks 数据库上启用 Service Broker，请执行下面的 Transact-SQL 语句  ：  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
为了使查询通知示例正确运行，必须在数据库服务器上执行以下 Transact-SQL 语句。  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>查询通知权限  
执行请求通知的命令的用户必须具有对服务器的 SUBSCRIBE QUERY NOTIFICATIONS 数据库权限。  
  
在部分信任情况下运行的客户端代码需要 <xref:Microsoft.Data.SqlClient.SqlClientPermission>。  
  
以下代码创建 <xref:Microsoft.Data.SqlClient.SqlClientPermission> 对象，并将 <xref:System.Security.Permissions.PermissionState> 设置为 <xref:System.Security.Permissions.PermissionState.Unrestricted>。 如果未对调用堆栈中处于较高位置的所有调用方授予权限，<xref:System.Security.CodeAccessPermission.Demand%2A> 会在运行时强制执行 <xref:System.Security.SecurityException>。  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>选择通知对象  
查询通知 API 提供两个用于处理通知的对象：<xref:Microsoft.Data.SqlClient.SqlDependency> 和 <xref:Microsoft.Data.Sql.SqlNotificationRequest>。
  
### <a name="using-sqldependency"></a>使用 SqlDependency  
要使用 <xref:Microsoft.Data.SqlClient.SqlDependency>，必须对所使用的 SQL Server 数据库启用 Service Broker，并且用户必须具有接收通知的权限。 Service Broker 对象（如通知队列）是预定义的。  
  
此外，<xref:Microsoft.Data.SqlClient.SqlDependency> 会自动启动一个工作线程以在通知发布到队列中时处理这些通知；它还会分析 Service Broker 消息，将此信息作为事件参数数据公开。 必须通过调用 <xref:Microsoft.Data.SqlClient.SqlDependency> 方法建立对数据库的依赖关系，从而初始化 `Start`。 这是一个静态方法，对于每个所需的数据库连接，在应用程序初始化期间仅需调用一次。 必须在应用程序终止时为执行的每个相关连接调用 `Stop` 方法。  
  
### <a name="using-sqlnotificationrequest"></a>使用 SqlNotificationRequest  
与此相反，<xref:Microsoft.Data.Sql.SqlNotificationRequest> 要求你自己实现整个侦听基础结构。 此外，必须定义队列所支持的所有支持 Service Broker 对象，例如队列、服务和消息类型。 如果你的应用程序需要特殊通知消息或通知行为，或者你的应用程序是较大的 Service Broker 应用程序的一部分，则此手动方法非常有用。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 中的查询通知](query-notifications-sql-server.md)