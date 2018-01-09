---
title: "使用事务 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a8beed22985c5f73ff5a4c1fed722fb331155ada
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="using-transactions"></a>使用事务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]管理对象 (SMO)，可以通过连接到的实例来实现事务处理[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用<xref:Microsoft.SqlServer.Management.Common.ServerConnection>对象。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>对象由引用<xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>属性<xref:Microsoft.SqlServer.Management.Smo.Server>对象建立连接时。 <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> 等方法均属于 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 对象属性。  
  
## <a name="see-also"></a>另请参阅  
 [创建 SMO 程序](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
