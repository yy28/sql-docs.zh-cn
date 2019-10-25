---
title: ADO.NET 中的 SQL Server 数据操作
description: 介绍如何使用 SQL Server 中的数据。 包含有关大容量复制操作、MARS、异步操作和表值参数的部分。
ms.date: 08/15/2019
ms.assetid: b864ebc9-ed8e-4059-85fd-36d9198f5521
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: ed9beea680575bba7fb01fc56af147e20b39218a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452041"
---
# <a name="sql-server-data-operations-in-adonet"></a>ADO.NET 中的 SQL Server 数据操作

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

本部分介绍适用于 SQL Server （<xref:Microsoft.Data.SqlClient>）的 Microsoft SqlClient 数据提供程序 SQL Server 特性和功能。  
  
## <a name="in-this-section"></a>在本节中  
[SQL Server 中的大容量复制操作](bulk-copy-operations-sql-server.md)  
介绍适用于 SQL Server 的 .NET 数据提供程序的大容量复制功能。  
  
[多重活动结果集 (MARS)](multiple-active-result-sets-mars.md)  
描述当从单独的命令启动 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的每个实例时，如何在一个连接上打开多个 <xref:Microsoft.Data.SqlClient.SqlDataReader>。  
  
[异步操作](asynchronous-operations.md)  
介绍如何使用根据 .NET Framework 所使用的异步模型建模的 API 执行异步数据库操作。  
  
[表值参数](table-valued-parameters.md)  
介绍如何使用 SQL Server 2008 中引入的表值参数。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
