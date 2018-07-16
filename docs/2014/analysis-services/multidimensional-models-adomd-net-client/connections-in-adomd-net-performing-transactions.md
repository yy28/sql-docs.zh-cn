---
title: 在 ADOMD.NET 中执行事务 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- transactions [ADOMD.NET]
- ADOMD.NET, transactions
- AdomdTransaction object
ms.assetid: 7978c28b-c255-43c0-ad05-f38604d4d8fe
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04157786e3a3d9349c2f1e324291a3a0bda5928d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167588"
---
# <a name="performing-transactions-in-adomdnet"></a>在 ADOMD.NET 中执行事务
  在 ADOMD.NET 中，可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 对象管理给定 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象的事务上下文。 使用此功能可在同一上下文中运行多个命令。 每个命令将读取相同的数据，在每个命令执行之间不会更改读取的数据。  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 类是 `System.Data.IDbTransaction` 接口的实现，该类是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 类库的一部分且通过支持事务的所有 .NET Framework 数据访问接口实现。  
  
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
  
## <a name="see-also"></a>请参阅  
 [在 ADOMD.NET 中建立连接](connections-in-adomd-net.md)   
 [ADOMD.NET 客户端编程](adomd-net-client-programming.md)  
  
  
