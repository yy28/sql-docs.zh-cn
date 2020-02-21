---
title: SQL Server 中的查询通知
description: 介绍当数据发生更改时，.NET 应用程序如何从 SQL Server 请求通知。
ms.date: 08/15/2019
ms.assetid: 0f0ba1a1-3180-4af8-87f7-c795dc8f8f55
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 9bcce207ed8427343e739959c9e91b988d9675cc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251185"
---
# <a name="query-notifications-in-sql-server"></a>SQL Server 中的查询通知

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

查询通知建立在 Service Broker 基础结构之上，并允许在数据发生更改时向应用程序发送通知。 对提供数据库信息的缓存且需要在源数据发生更改时收到通知的应用程序（如 Web 应用程序）而言，以上功能特别有用。  
  
使用 ADO.NET，可以通过三种方式实现查询通知：  
  
- 公开服务器端功能的 `SqlNotificationRequest` 类提供低级别实现，使你能够利用通知请求执行命令。  
  
- 高级别实现由 `SqlDependency` 类提供，该类可提供源应用程序与 SQL Server 之间的通知功能的高级抽象，使你能够使用依赖项来检测服务器中的更改。 大多数情况下，这是托管客户端应用程序通过用于 SQL Server 的 Microsoft SqlClient 数据提供程序利用 SQL Server 通知功能的最简单、最有效的方法。  
  
- 此外，使用 ASP.NET 2.0 或更高版本构建的 Web 应用程序可以使用 `SqlCacheDependency` 帮助程序类。  
  
如果应用程序需要通过刷新显示或缓存来响应基础数据中的更改，则查询通知非常有用。 如果执行相同命令生成的结果集与最初检索到的结果集不同，则 Microsoft SQL Server 可允许 .NET 应用程序向 SQL Server 发送命令和请求通知。 服务器上生成的通知是通过这些队列发送的，以便在稍后进行处理。  
  
可以为 SELECT 和 EXECUTE 语句设置通知。 使用 EXECUTE 语句时，SQL Server 将为执行的命令（而不是 EXECUTE 语句本身）注册一个通知。 命令必须满足 SELECT 语句的要求和限制。 当注册通知的命令包含多条语句时，数据库引擎将为批处理中的每条语句创建一个通知。  
  
如果你正在开发需要在数据发生更改时提供可靠的次秒级通知的应用程序，请查看 SQL Server 联机丛书中[计划通知](https://go.microsoft.com/fwlink/?LinkId=211984)主题中的“计划高效的查询通知策略”和“查询通知的替代方法”部分   。 有关查询通知和 SQL Server Service Broker 的详细信息，请参阅以下指向 SQL Server 联机丛书中主题的链接。  
  
**SQL Server 文档**  
  
- [使用查询通知](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms175110(v=sql.105))  
  
- [为通知创建查询](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [开发 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522889(v=sql.105))  
  
- [Service Broker 开发人员信息中心](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [开发人员指南 (Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="in-this-section"></a>在本节中  
[启用查询通知](enable-query-notifications.md)  
介绍如何使用查询通知，其中包括启用和使用查询通知的要求。  
  
[ASP.NET 应用程序中的 SqlDependency](sqldependency-aspnet-app.md)  
演示如何使用 ASP.NET 应用程序中的查询通知。  
  
[使用 SqlDependency 检测更改](detect-changes-sqldependency.md)  
演示如何检测查询结果与最初接收的结果不同的情况。  
  
[使用 SqlNotificationRequest 执行 SqlCommand](sqlcommand-execution-sqlnotificationrequest.md)  
演示如何将 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象配置为使用查询通知。  
  
## <a name="reference"></a>参考  
<xref:Microsoft.Data.Sql.SqlNotificationRequest>  
介绍 <xref:Microsoft.Data.Sql.SqlNotificationRequest> 类及其所有成员。  
  
<xref:Microsoft.Data.SqlClient.SqlDependency>  
介绍 <xref:Microsoft.Data.SqlClient.SqlDependency> 类及其所有成员。  
  
<xref:System.Web.Caching.SqlCacheDependency>  
介绍 <xref:System.Web.Caching.SqlCacheDependency> 类及其所有成员。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
