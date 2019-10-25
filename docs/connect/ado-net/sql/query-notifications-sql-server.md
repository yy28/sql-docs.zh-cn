---
title: SQL Server 中的查询通知
description: 介绍当数据发生更改时，.NET 应用程序如何从 SQL Server 请求通知。
ms.date: 08/15/2019
ms.assetid: 0f0ba1a1-3180-4af8-87f7-c795dc8f8f55
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d47241e3656e3ca7b4f5ea0eebe9f2cc8b571bf6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452071"
---
# <a name="query-notifications-in-sql-server"></a>SQL Server 中的查询通知

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

查询通知建立在 Service Broker 基础结构之上，并允许在数据发生更改时向应用程序发送通知。 对提供数据库信息的缓存且需要在源数据发生更改时收到通知的应用程序（如 Web 应用程序）而言，以上功能特别有用。  
  
可以通过三种方式使用 ADO.NET 实现查询通知：  
  
- 低级别实现由公开服务器端功能的 `SqlNotificationRequest` 类提供，使你能够使用通知请求执行命令。  
  
- 高级别实现由 `SqlDependency` 类提供，该类提供源应用程序与 SQL Server 之间的通知功能的高级抽象，使你能够使用依赖项来检测服务器中的更改。 大多数情况下，这是托管客户端应用程序通过用于 SQL Server 的 Microsoft SqlClient 数据提供程序利用 SQL Server 通知功能的最简单、最有效的方法。  
  
- 此外，使用 ASP.NET 2.0 或更高版本构建的 Web 应用程序可以使用 `SqlCacheDependency` 帮助程序类。  
  
查询通知用于需要刷新显示或缓存以响应基础数据更改的应用程序。 如果执行相同命令生成的结果集与最初检索到的结果集不同，则 Microsoft SQL Server 可允许 .NET 应用程序向 SQL Server 发送命令和请求通知。 服务器上生成的通知是通过这些队列发送的，以便在稍后进行处理。  
  
您可以为 SELECT 和 EXECUTE 语句设置通知。 使用 EXECUTE 语句时，SQL Server 会注册已执行命令的通知，而不是执行语句本身。 命令必须满足 SELECT 语句的要求和限制。 当注册通知的命令包含多条语句时，数据库引擎将为批处理中的每条语句创建一个通知。  
  
如果你正在开发需要在数据发生更改时提供可靠的次秒级通知的应用程序，请查看 SQL Server 联机丛书中[计划通知](https://go.microsoft.com/fwlink/?LinkId=211984)主题中的“计划高效的查询通知策略”和“查询通知的替代方法”部分   。 有关查询通知和 SQL Server Service Broker 的详细信息，请参阅以下指向 SQL Server 联机丛书中主题的链接。  
  
**SQL Server 文档**  
  
- [使用查询通知](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms175110(v=sql.105))  
  
- [为通知创建查询](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [开发 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522889(v=sql.105))  
  
- [Service Broker 开发人员信息中心](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [开发人员指南 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="in-this-section"></a>在本节中  
[启用查询通知](enable-query-notifications.md)  
介绍如何使用查询通知（包括启用和使用查询通知的要求）。  
  
[ASP.NET 应用程序中的 SqlDependency](sqldependency-aspnet-app.md)  
演示如何从 ASP.NET 应用程序使用查询通知。  
  
[使用 SqlDependency 检测更改](detect-changes-sqldependency.md)  
演示如何检测查询结果与最初接收的结果不同。  
  
[使用 SqlNotificationRequest 执行 SqlCommand](sqlcommand-execution-sqlnotificationrequest.md)  
演示如何配置 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象以使用查询通知。  
  
## <a name="reference"></a>参考  
<xref:Microsoft.Data.Sql.SqlNotificationRequest>  
描述 <xref:Microsoft.Data.Sql.SqlNotificationRequest> 类及其所有成员。  
  
<xref:Microsoft.Data.SqlClient.SqlDependency>  
描述 <xref:Microsoft.Data.SqlClient.SqlDependency> 类及其所有成员。  
  
<xref:System.Web.Caching.SqlCacheDependency>  
描述 <xref:System.Web.Caching.SqlCacheDependency> 类及其所有成员。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
