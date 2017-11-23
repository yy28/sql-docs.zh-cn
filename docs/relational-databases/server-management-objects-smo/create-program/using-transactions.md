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
ms.technology: docset-sql-devref
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
ms.openlocfilehash: 93335b496f798658f2840a1a02757ed0949b9760
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="using-transactions"></a>使用事务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]管理对象 (SMO)，可以通过连接到的实例来实现事务处理[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用<xref:Microsoft.SqlServer.Management.Common.ServerConnection>对象。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>对象由引用<xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>属性<xref:Microsoft.SqlServer.Management.Smo.Server>对象建立连接时。 <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> 等方法均属于 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 对象属性。  
  
## <a name="see-also"></a>另请参阅  
 [创建 SMO 程序](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
