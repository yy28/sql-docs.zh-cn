---
title: 使用 SqlDependency 检测更改
description: 演示如何检测查询结果与最初接收的结果不同的情况。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 6a003670c15ac95b6f0a5f70d0997c1c854b089e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247824"
---
# <a name="detecting-changes-with-sqldependency"></a>使用 SqlDependency 检测更改

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

<xref:Microsoft.Data.SqlClient.SqlDependency> 对象可以与 <xref:Microsoft.Data.SqlClient.SqlCommand> 相关联，以便检测查询结果与最初检索到的结果不同的情况。 还可以为 `OnChange` 事件分配一个委托，该事件将在关联命令的结果变更时激发。 在执行命令之前，必须将 <xref:Microsoft.Data.SqlClient.SqlDependency> 与命令相关联。 <xref:Microsoft.Data.SqlClient.SqlDependency> 的 `HasChanges` 属性还可用于确定自第一次检索数据后，查询结果是否变更。

## <a name="security-considerations"></a>安全注意事项

依赖项基础结构依赖于调用 <xref:Microsoft.Data.SqlClient.SqlDependency.Start%2A> 时打开的 <xref:Microsoft.Data.SqlClient.SqlConnection>，以便接收已针对给定命令更改基础数据的通知。 客户端启动对 `SqlDependency.Start` 的调用的能力通过使用 <xref:Microsoft.Data.SqlClient.SqlClientPermission> 和代码访问安全性特性进行控制。 有关详细信息，请参阅[启用查询通知](enable-query-notifications.md)。

### <a name="example"></a>示例

以下步骤演示了如何声明依赖项、执行命令以及在结果集更改时接收通知：

1. 启动通向服务器的 `SqlDependency` 连接。

2. 创建 <xref:Microsoft.Data.SqlClient.SqlConnection> 和 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象以连接到服务器并定义 Transact-SQL 语句。

3. 创建新的 `SqlDependency` 对象或使用现有对象，然后将其绑定到 `SqlCommand` 对象。 在内部，这将创建一个 <xref:Microsoft.Data.Sql.SqlNotificationRequest> 对象，并根据需要将其绑定到命令对象。 此通知请求包含唯一标识此 `SqlDependency` 对象的内部标识符。 如果客户端侦听器尚未处于活动状态，它还会启动它。

4. 向 `SqlDependency` 对象的 `OnChange` 事件订阅事件处理程序。

5. 使用 `SqlCommand` 对象的任何 `Execute` 方法执行该命令。 因为该命令绑定到通知对象，所以服务器认识到它必须生成一个通知，并且队列信息将指向依赖项队列。

6. 停止与服务器的 `SqlDependency` 连接。

如果任何用户随后更改了基础数据，则 Microsoft SQL Server 将检测到存在此类更改的挂起通知，并发布通知，该通知通过调用 `SqlDependency.Start` 创建的基础 `SqlConnection` 进行处理并转发给客户端。 客户端侦听器接收失效消息。 然后，客户端侦听器查找关联的 `SqlDependency` 对象，并激发 `OnChange` 事件。

下面的代码段显示用于创建示例应用程序的设计模式。

```csharp
void Initialization()
{
    // Create a dependency connection.
    SqlDependency.Start(connectionString, queueName);
}

void SomeMethod()
{
    // Assume connection is an open SqlConnection.

    // Create a new SqlCommand object.
    using (SqlCommand command=new SqlCommand(
        "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers",
        connection))
    {

        // Create a dependency and associate it with the SqlCommand.
        SqlDependency dependency=new SqlDependency(command);
        // Maintain the reference in a class member.

        // Subscribe to the SqlDependency event.
        dependency.OnChange+=new
           OnChangeEventHandler(OnDependencyChange);

        // Execute the command.
        using (SqlDataReader reader = command.ExecuteReader())
        {
            // Process the DataReader.
        }
    }
}

// Handler method
void OnDependencyChange(object sender,
   SqlNotificationEventArgs e )
{
  // Handle the event (for example, invalidate this cache entry).
}

void Termination()
{
    // Release the dependency.
    SqlDependency.Stop(connectionString, queueName);
}
```

## <a name="next-steps"></a>后续步骤
- [SQL Server 中的查询通知](query-notifications-sql-server.md)
