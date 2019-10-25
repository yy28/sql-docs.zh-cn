---
title: 异步操作
description: 介绍如何使用根据 .NET Framework 所使用的异步模型建模的 API 执行异步数据库操作。
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 79cde936328476408fabb3df7a6bff8d983ace1c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452320"
---
# <a name="asynchronous-operations"></a>异步操作

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

某些数据库操作（例如命令执行）可能需要很长时间才能完成。 在这种情况下，单线程应用程序必须阻止其他操作，并等待命令完成，然后才能继续执行自己的操作。 与此相反，通过将长时间运行的操作分配给后台线程，允许前台线程在操作过程中保持活动状态。 例如，在 Windows 应用程序中，将长时间运行的操作委托给后台线程允许用户界面线程在执行操作时保持响应。  
  
.NET 提供了几种标准异步设计模式，开发人员可以使用这些模式来利用后台线程，并释放用户界面或高优先级的线程以完成其 <xref:Microsoft.Data.SqlClient.SqlCommand> 类中的其他操作。 具体而言，<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 和 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 方法，与 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> 和 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A> 方法配对，则提供异步支持。  
  
> [!NOTE]
>  异步编程是 .NET 的核心功能。 有关可供开发人员使用的不同异步技术的详细信息，请参阅[以异步方式调用同步方法](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)。  
  
尽管使用带有 ADO.NET 功能的异步技术不会添加任何特别的注意事项，但请务必注意创建多线程应用程序的优点和缺陷。 本部分中的示例指出了开发人员在构建合并了多线程功能的应用程序时需要考虑的几个重要问题。  
  
## <a name="in-this-section"></a>在本节中  
[使用回调的 Windows 应用程序](windows-applications-callbacks.md)  
提供一个示例，演示如何安全地执行异步命令，以及如何在单独的线程中正确地处理与窗体及其内容的交互。  
  
[使用等待句柄的 ASP.NET 应用程序](aspnet-apps-use-wait-handles.md)  
提供一个示例，演示如何通过 ASP.NET 页执行多个并发命令，并使用等待句柄来管理所有命令完成时的操作。  
  
[在控制台应用程序中轮询](poll-console-applications.md)  
提供一个示例，演示如何使用轮询等待从控制台应用程序中完成异步命令执行。 此方法也适用于类库或其他不带用户界面的应用程序。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
- [以异步方式调用同步方法](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)
