---
description: 使用事务
title: 使用事务 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4e12a321436f13b6db9ae7c5a63f29a6d69766b0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420291"
---
# <a name="using-transactions"></a>使用事务
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理对象 (SMO) 中，通过使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例，进而实现事务处理。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>建立连接后，对象由 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 对象的属性引用 <xref:Microsoft.SqlServer.Management.Smo.Server> 。 <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> 等方法均属于 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 对象属性。  
  
## <a name="see-also"></a>另请参阅  
 [创建 SMO 程序](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
