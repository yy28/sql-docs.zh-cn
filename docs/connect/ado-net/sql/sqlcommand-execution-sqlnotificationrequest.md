---
title: 使用 SqlNotificationRequest 执行 SqlCommand
description: 演示如何将 SqlCommand 对象配置为使用查询通知。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 1ad2fd2f29c7218d1da0535ca089e2648d4b0cf0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80918687"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>使用 SqlNotificationRequest 执行 SqlCommand

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

可以将 <xref:Microsoft.Data.SqlClient.SqlCommand> 配置为在数据从服务器中提取后发生更改时生成通知，如果再次执行查询，结果集将不同。 这对于以下情况非常有用：你希望在服务器上使用自定义通知队列，或者不希望维护活动对象的情况。

## <a name="creating-the-notification-request"></a>创建通知请求

可以使用 <xref:Microsoft.Data.Sql.SqlNotificationRequest> 对象，通过将通知请求绑定到 `SqlCommand` 对象来创建请求。 创建请求后，你将不再需要 `SqlNotificationRequest` 对象。 可以在队列中查询任何通知，并做出相应响应。 即使应用程序关闭后重新启动，也会出现通知。

在对关联通知执行命令时，对原始结果集所做的任何更改都会触发向在通知请求中配置的 SQL Server 队列发送消息。

如何轮询 SQL Server 队列和解释该消息是应用程序特定的。 应用程序负责轮询队列并根据消息的内容做出响应。

> [!NOTE]
> 在 <xref:Microsoft.Data.SqlClient.SqlDependency> 中使用 SQL Server 通知请求时，请创建自己的队列名称，而不是使用默认的服务名称。

<xref:Microsoft.Data.Sql.SqlNotificationRequest> 没有新的客户端安全元素。 这主要是一种服务器功能，并且服务器已创建用户必须拥有的用于请求通知的特殊权限。

### <a name="example"></a>示例

下面的代码段演示如何创建 <xref:Microsoft.Data.Sql.SqlNotificationRequest> 并将其与 <xref:Microsoft.Data.SqlClient.SqlCommand> 相关联。

```csharp
// Assume connection is an open SqlConnection.
// Create a new SqlCommand object.
SqlCommand command=new SqlCommand(
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);

// Create a SqlNotificationRequest object.
SqlNotificationRequest notificationRequest=new SqlNotificationRequest();
notificationRequest.id="NotificationID";
notificationRequest.Service="mySSBQueue";

// Associate the notification request with the command.
command.Notification=notificationRequest;
// Execute the command.
command.ExecuteReader();
// Process the DataReader.
// You can use Transact-SQL syntax to periodically poll the
// SQL Server queue to see if you have a new message.
```

## <a name="next-steps"></a>后续步骤
- [SQL Server 中的查询通知](query-notifications-sql-server.md)
