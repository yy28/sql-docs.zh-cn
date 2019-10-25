---
title: ASP.NET 应用程序中的 SqlDependency
description: 演示如何从 ASP.NET 应用程序使用查询通知。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2115d087d837118b99ee3ffded9cae0003b6d4e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451960"
---
# <a name="sqldependency-in-an-aspnet-application"></a>ASP.NET 应用程序中的 SqlDependency

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

本节中的示例演示如何通过利用 ASP.NET <xref:System.Web.Caching.SqlCacheDependency> 对象间接使用 <xref:Microsoft.Data.SqlClient.SqlDependency>。 @No__t_0 对象使用 <xref:Microsoft.Data.SqlClient.SqlDependency> 侦听通知并正确更新缓存。  
  
> [!NOTE]
>  示例代码假定您已通过执行[启用查询通知](enable-query-notifications.md)中的脚本启用了查询通知。  
  
## <a name="about-the-sample-application"></a>关于示例应用程序  
示例应用程序使用单个 ASP.NET 网页在 <xref:System.Web.UI.WebControls.GridView> 控件中显示 AdventureWorks SQL Server 数据库中的产品信息  。 加载页面时，代码会将当前时间写入 <xref:System.Web.UI.WebControls.Label> 控件。 然后，它定义一个 <xref:System.Web.Caching.SqlCacheDependency> 对象并设置 <xref:System.Web.Caching.Cache> 对象的属性，以存储最多三分钟的缓存数据。 然后，该代码将连接到数据库并检索数据。 加载页面并运行应用程序时，ASP.NET 将从缓存中检索数据，可以通过注意页面上的时间未更改来进行验证。 如果被监视的数据发生更改，则 ASP.NET 会使缓存失效，并用新数据重新填充 `GridView` 控件，更新 `Label` 控件中显示的时间。  
  
## <a name="creating-the-sample-application"></a>创建示例应用程序  
按照以下步骤创建并运行示例应用程序：  
  
1. 创建新的 ASP.NET 网站。  
  
2. 将 <xref:System.Web.UI.WebControls.Label> 和 <xref:System.Web.UI.WebControls.GridView> 控件添加到 default.aspx 页。  
  
3. 打开页的类模块并添加以下指令：  
  
    ```csharp  
    using Microsoft.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. 在页面的 `Page_Load` 事件中添加以下代码：  
  
    [!code-csharp[DataWorks SqlDependency_Start#1](~/../sqlclient/doc/samples/SqlDependency_Start.cs#1)]
  
5. 添加两个帮助器方法： `GetConnectionString` 和 `GetSQL`。 已定义的连接字符串使用集成安全性。 你将需要验证所使用的帐户是否具有必要的数据库权限，并且示例数据库 AdventureWorks 是否启用了通知  。
  
    [!code-csharp[DataWorks SqlDependency_Start#2](~/../sqlclient/doc/samples/SqlDependency_Start.cs#2)]
  
### <a name="testing-the-application"></a>测试应用程序  
应用程序会缓存 Web 窗体上显示的数据，如果没有任何活动，则每三分钟刷新一次。 如果数据库发生了更改，则立即刷新缓存。 从 Visual Studio 运行应用程序，该应用程序会将页面加载到浏览器中。 显示的缓存刷新时间指示上次刷新缓存的时间。 等待三分钟，然后刷新页面，导致回发事件发生。 请注意，页面上显示的时间已更改。 如果在3分钟内刷新页面，则页面上显示的时间将保持不变。  
  
现在使用 Transact-sql UPDATE 命令更新数据库中的数据并刷新页面。 此时显示的时间表示缓存是通过数据库中的新数据刷新的。 请注意，虽然缓存已更新，但在回发事件发生之前，页面上显示的时间不会更改。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 中的查询通知](query-notifications-sql-server.md)
