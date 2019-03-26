---
title: ADO.NET 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetconnection.f1
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d5811c4ea89a177f9862f27ba75f6baaddef7208
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58272383"
---
# <a name="adonet-connection-manager"></a>ADO.NET 连接管理器
  [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器使包能够使用 .NET 访问接口访问数据源。 此连接管理器通常用于访问 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]等数据源，也用于访问在用 C# 等语言以托管代码编写的自定义任务中通过 OLE DB 和 XML 公开的数据源。  
  
 将 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器添加到包时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建在运行时作为 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接进行解析的连接管理器，同时还会设置该连接管理器的属性，并将该连接管理器添加到包的 **Connections** 集合。  
  
 该连接管理器的 **ConnectionManagerType** 属性设置为 **ADO.NET**。 **ConnectionManagerType** 的值受到限定，以包含连接管理器所使用的 .NET 访问接口的名称。  
  
## <a name="adonet-connection-manager-troubleshooting"></a>ADO.NET 连接管理器故障排除  
 可以记录 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器对外部数据访问接口所做的调用。 使用此日志记录功能，可以对 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器与外部数据源的连接进行故障排除。 若要记录 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器在读取数据时，某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期数据类型的数据将生成下表中显示的结果。  
  
|SQL Server 数据类型|结果|  
|--------------------------|------------|  
|**time**、 **datetimeoffset**|除非包使用参数化 SQL 命令，否则，包将失败。 若要使用参数化 SQL 命令，请在包中使用执行 SQL 任务。 有关详细信息，请参阅 [执行 SQL 任务](../../integration-services/control-flow/execute-sql-task.md) 和 [执行 SQL 任务中的参数和返回代码](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)。|  
|**datetime2**|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器截断毫秒值。|  
  
> [!NOTE]  
>  有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和它们如何映射到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型的详细信息，请参阅[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md) 和 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="adonet-connection-manager-configuration"></a>配置 ADO.NET 连接管理器  
 可以通过下列方式配置 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器：  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
-   提供配置为满足选定 .NET 访问接口的要求的特定连接字符串。  
  
-   包括要连接到的数据源的名称（取决于访问接口）。  
  
-   为选定的访问接口提供相应的安全凭据。  
  
-   指示是否在运行时保留从连接管理器中创建的连接。  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器的许多配置选项取决于该连接管理器所使用的 .NET 访问接口。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题之一：  
  
-   [配置 ADO.NET 连接管理器](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
## <a name="configure-adonet-connection-manager"></a>配置 ADO.NET 连接管理器
  可以使用 **“配置 ADO.NET 连接管理器”** 对话框，添加与可使用 .NET Framework 数据访问接口（例如，SqlClient 访问接口）访问的数据源之间的连接。 连接管理器可使用现有连接，或者您也可以创建一个新的连接。  
  
 若要了解有关 ADO.NET 连接管理器的详细信息，请参阅 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)。  
  
### <a name="options"></a>选项  
 **数据连接**  
 从列表中选择一个现有的 ADO.NET 数据连接。  
  
 **数据连接属性**  
 查看所选 ADO.NET 数据连接的属性和值。  
  
 **新建**  
 通过使用“连接管理器”对话框创建 ADO.NET 数据连接。  
  
 **删除**  
 选择某个连接，然后可以使用“删除”按钮将其删除。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 连接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
