---
title: ADO.NET 中的 SQL Server 数据操作
description: 介绍如何使用 SQL Server 中的数据。 包含有关大容量复制操作、MARS、异步操作和表值参数的部分。
ms.date: 08/15/2019
ms.assetid: b864ebc9-ed8e-4059-85fd-36d9198f5521
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: f6e842b38291fb704828b9b5a70d0652cfda51e0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920983"
---
# <a name="sql-server-data-operations-in-adonet"></a>ADO.NET 中的 SQL Server 数据操作

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

本节介绍了特定于 Microsoft SqlClient Data Provider for SQL Server 的 SQL Server 特性和功能 (<xref:Microsoft.Data.SqlClient>)。  
  
## <a name="in-this-section"></a>在本节中  
[SQL Server 中的大容量复制操作](bulk-copy-operations-sql-server.md)  
介绍适用于 SQL Server 的 .NET 数据提供程序的大容量复制功能。  
  
[多重活动结果集 (MARS)](multiple-active-result-sets-mars.md)  
介绍当从单独的命令启动 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的每个实例时，如何在一个连接上打开多个 <xref:Microsoft.Data.SqlClient.SqlDataReader>。  
  
[异步操作](asynchronous-operations.md)  
介绍如何使用根据 .NET Framework 所使用的异步模型建模的 API 执行异步数据库操作。  
  
[表值参数](table-valued-parameters.md)  
介绍如何使用在 SQL Server 2008 中引入的表值参数。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
