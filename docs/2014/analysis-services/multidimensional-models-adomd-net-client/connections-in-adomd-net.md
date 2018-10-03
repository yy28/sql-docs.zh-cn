---
title: 在 ADOMD.NET 中建立连接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- opening connections
- closing connections
- connections [ADOMD.NET]
- ADOMD.NET, connections
ms.assetid: 7b9610f5-6641-42cc-af4e-bd35771913d1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a338d1902440fe6489b7c4c91176899999aa25fc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172017"
---
# <a name="establishing-connections-in-adomdnet"></a>在 ADOMD.NET 中建立连接
  在 ADOMD.NET 中，使用<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>对象以连接打开与分析数据源，如[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 不再需要连接时，应显式关闭该连接。  
  
## <a name="opening-a-connection"></a>打开连接  
 若要在 ADOMD.NET 中打开连接，您必须首先指定一个指向有效分析数据源和数据库的连接字符串。 然后，必须显式打开与该数据源的连接。  
  
### <a name="specifying-a-multidimensional-data-source"></a>指定多维数据源  
 若要指定分析数据源和数据库，需设置 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 属性。 为 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 属性指定的连接字符串为兼容 OLE DB 的字符串。 ADOMD.NET 使用指定的连接字符串确定连接到服务器的方式。  
  
 可对现有的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 对象设置 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 属性，或者可在创建 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象的实例期间进行设置。 下面的代码演示如何在创建 ADOMD 连接时设置 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 属性：  
  
```vb  
Dim advwrksConnection As New AdomdConnection("Data Source=localhost;Catalog=AdventureWorksAS")  
System.Diagnostics.Debug.Writeline(advwrksConnection.ConnectionString)  
```  
  
```csharp  
AdomdConnection advwrksConnection = new AdomdConnection("Data Source=localhost;Catalog=AdventureWorksAS");  
System.Diagnostics.Debug.Writeline(advwrksConnection.ConnectionString);  
```  
  
### <a name="opening-a-connection-to-the-data-source"></a>打开与数据源的连接  
 指定连接字符串后，必须使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 方法打开连接。 打开 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象时，可对连接设置各种安全级别。 用于连接的安全级别取决于 `ProtectionLevel` 连接字符串设置的值。 在 ADOMD.NET 中打开安全连接的详细信息，请参阅[在 ADOMD.NET 中建立安全连接](connections-in-adomd-net-establishing-secure-connections.md)。  
  
## <a name="working-with-a-connection"></a>使用连接  
 每个打开的连接存在于会话中，它可为有状态的操作提供支持。 一个会话可由多个打开的连接共享。 共享会话可使多个客户端共享同一上下文。 有关详细信息，请参阅[使用连接和会话在 ADOMD.NET 中](../multidimensional-models-adomd-net-client/connections-in-adomd-net-working-with-connections-and-sessions.md)。  
  
 您可以使用打开的连接检索元数据和数据，并运行命令。 有关详细信息，请参阅[分析数据源中检索元数据](retrieving-metadata-from-an-analytical-data-source.md)，[从分析的数据源检索数据](retrieving-data-from-an-analytical-data-source.md)，和[执行命令对分析数据源](executing-commands-against-an-analytical-data-source.md)。  
  
 连接打开时，您可以检索数据和元数据，并从已提交读事务中运行命令，在该事务中读取数据时将保持共享锁以避免脏读。 但在事务结束之前仍可更改数据，从而产生不可重复的读取或虚拟数据。 有关详细信息，请参阅[在 ADOMD.NET 中执行事务](../../relational-databases/native-client-ole-db-transactions/transactions.md)。  
  
## <a name="closing-a-connection"></a>关闭连接  
 当您不再需要连接时，建议您显式关闭 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象。 若要显式关闭连接，请使用 `Close` 对象的 `Dispose` 和 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 方法。  
  
 未显式关闭、但允许离开作用域的连接，可能不会足够快速地释放服务器资源来启用高并发 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 客户端应用程序以有效地打开新连接。 如果未显式关闭连接，则 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象使用的会话可保持活动状态，具体取决于连接的创建方式。  
  
 有关会话的详细信息，请参阅[使用连接和会话在 ADOMD.NET 中](../multidimensional-models-adomd-net-client/connections-in-adomd-net-working-with-connections-and-sessions.md)。  
  
> [!IMPORTANT]  
>  在任何实现的类的 `Finalize` 方法中，不要调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象、<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 对象或任何其他托管对象的 `Close` 或 `Dispose` 方法。 在终结器中，应仅释放实现的类直接拥有的非托管资源。 如果实现的类未拥有任何非托管资源，则不要在类定义中包括 `Finalize` 方法。  
  
## <a name="see-also"></a>请参阅  
 [ADOMD.NET 客户端编程](adomd-net-client-programming.md)  
  
  
