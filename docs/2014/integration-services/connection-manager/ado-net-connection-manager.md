---
title: ADO.NET 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a94c611a8c200f5b7b8211b6a1d69b3f147b7a37
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37195657"
---
# <a name="adonet-connection-manager"></a>ADO.NET 连接管理器
  [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器使包能够使用 .NET 访问接口访问数据源。 此连接管理器通常用于访问 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]等数据源，也用于访问在用 C# 等语言以托管代码编写的自定义任务中通过 OLE DB 和 XML 公开的数据源。  
  
 当您将添加[!INCLUDE[vstecado](../../includes/vstecado-md.md)]到包，连接管理器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建的连接管理器，它将被解析为[!INCLUDE[vstecado](../../includes/vstecado-md.md)]连接在运行时，设置该连接管理器属性，并将添加到连接管理器`Connections`上包的集合。  
  
 `ConnectionManagerType`连接管理器属性设置为`ADO.NET`。 值`ConnectionManagerType`受到限定，以包括连接管理器使用的.NET 提供程序的名称。  
  
## <a name="adonet-connection-manager-troubleshooting"></a>ADO.NET 连接管理器故障排除  
 可以记录 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器对外部数据访问接口所做的调用。 使用此日志记录功能，可以对 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器与外部数据源的连接进行故障排除。 若要记录 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器在读取数据时，某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期数据类型的数据将生成下表中显示的结果。  
  
|SQL Server 数据类型|结果|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|除非包使用参数化 SQL 命令，否则，包将失败。 若要使用参数化 SQL 命令，请在包中使用执行 SQL 任务。 有关详细信息，请参阅 [执行 SQL 任务](../control-flow/execute-sql-task.md) 和 [执行 SQL 任务中的参数和返回代码](../parameters-and-return-codes-in-the-execute-sql-task.md)。|  
|`datetime2`|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器截断毫秒值。|  
  
> [!NOTE]  
>  有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和它们如何映射到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型的详细信息，请参阅[数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql) 和 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="adonet-connection-manager-configuration"></a>配置 ADO.NET 连接管理器  
 可以通过下列方式配置 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器：  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
-   提供配置为满足选定 .NET 访问接口的要求的特定连接字符串。  
  
-   包括要连接到的数据源的名称（取决于访问接口）。  
  
-   为选定的访问接口提供相应的安全凭据。  
  
-   指示是否在运行时保留从连接管理器中创建的连接。  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器的许多配置选项取决于该连接管理器所使用的 .NET 访问接口。  
  
 有关可以在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题之一：  
  
-   [配置 ADO.NET 连接管理器](../configure-ado-net-connection-manager.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>并[连接以编程方式添加](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services &#40;SSIS&#41;的连接](integration-services-ssis-connections.md)  
  
  
