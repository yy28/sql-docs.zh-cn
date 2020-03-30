---
title: SQL Server 和 ADO.NET
description: 描述如何使用特定于 SQL Server 的功能
ms.date: 10/15/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e953d15c46459e0bd076cc85e9bc7bc65cae9d7c
ms.sourcegitcommit: 700c07312d1ffc034e7a684cbf4265afc7c84993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "78896717"
---
# <a name="sql-server-and-adonet"></a>SQL Server 和 ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

## <a name="microsoftdatasqlclient"></a>Microsoft.Data.SqlClient

<xref:Microsoft.Data.SqlClient> 提供对 SQL Server 各版本的访问权限，这些版本封装有数据库特定的协议。 <xref:Microsoft.Data.SqlClient> 包含一个表格格式数据流 (TDS) 分析程序，它用于直接与 SQL Server 通信。  
  
> [!NOTE]
> 要使用 SQL Server 的 Microsoft SqlClient 数据提供程序，应用程序必须引用 <xref:Microsoft.Data.SqlClient> 命名空间。  
  
## <a name="in-this-section"></a>在本节中  
[SQL Server 安全性](sql-server-security.md)  
简要介绍 SQL Server 安全功能，以及创建面向 SQL Server 的安全 ADO.NET 应用程序的应用程序方案。  
  
[SQL Server 数据类型和 ADO.NET](sql-server-data-types.md)  
介绍如何使用 SQL Server 数据类型，以及它们如何与 .NET 数据类型交互。  
  
[SQL Server 二进制和大值数据](sql-server-binary-large-value-data.md)  
介绍如何在 SQL Server 中使用大值数据。  
  
[ADO.NET 中的 SQL Server 数据操作](sql-server-data-operations.md)  
介绍如何使用 SQL Server 中的数据。 包含有关大容量复制操作、MARS、异步操作和表值参数的部分。  
  
[SQL Server 功能和 ADO.NET](sql-server-features-adonet.md)  
介绍对 ADO.NET 应用程序开发人员而言有用的 SQL Server 功能。  
  
有关 SQL Server 数据库引擎的完整文档，请参见你正在使用的 SQL Server 版本的 SQL Server 联机丛书。  
  
[QL Server 联机丛书](../../../sql-server/index.yml)
