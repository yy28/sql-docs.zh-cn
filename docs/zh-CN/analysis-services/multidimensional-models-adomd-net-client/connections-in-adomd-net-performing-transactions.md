---
title: In ADOMD.NET 执行事务 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 872d7aca21569018180e537c635032a9d036e3dd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connections-in-adomdnet---performing-transactions"></a>Connections in ADOMD.NET-执行事务
  在 ADOMD.NET 中，可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 对象管理给定 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象的事务上下文。 使用此功能可在同一上下文中运行多个命令。 每个命令将读取相同的数据，在每个命令执行之间不会更改读取的数据。  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>类是实现**System.Data.IDbTransaction**接口的一部分[!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework 类库和实现的所有.NET Framework 数据提供程序支持事务。  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 对象仅支持已提交读事务，在这些事务中读取数据时将保持共享锁以避免脏读。  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 用于启动该事务。 若要使用该事务，可随后对已启动该事务的连接运行命令。 结束使用此事务后，可回滚或提交该事务。  
  
## <a name="starting-a-transaction"></a>启动事务  
 可通过调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> 方法创建 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象的实例。 下面的示例演示如何创建 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 对象的实例：  
  
```  
Dim objTransaction As AdomdTransaction = objConnection.BeginTransaction()  
AdomdTransaction objTransaction = objConnection.BeginTransaction();  
```  
  
## <a name="rolling-back-a-transaction"></a>回滚事务  
 若要回滚现有的不完整事务，请调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Rollback%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 方法。 如果对现有的完整事务调用此方法，则将引发异常。  
  
## <a name="committing-a-transaction"></a>提交事务  
 调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> 方法来启动事务后，可通过调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Commit%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 方法完成该事务。 如果已对现有的完整事务调用此方法，则将引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [建立 Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)   
 [ADOMD.NET 客户端编程](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
