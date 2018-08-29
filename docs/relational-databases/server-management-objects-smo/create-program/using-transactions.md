---
title: 使用事务 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 94e0fe547c96351a0b00bfa39dcca0f6379016c5
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079272"
---
# <a name="using-transactions"></a>使用事务
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理对象 (SMO) 中，通过使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例，进而实现事务处理。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>引用的对象<xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>属性的<xref:Microsoft.SqlServer.Management.Smo.Server>时建立的连接对象。 <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> 等方法均属于 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 对象属性。  
  
## <a name="see-also"></a>请参阅  
 [创建 SMO 程序](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
