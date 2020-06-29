---
title: ADO 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fb4b667733f81eebbaf2b6a2ab9b205c09fe2c66
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85434534"
---
# <a name="ado-connection-manager"></a>ADO 连接管理器
  ADO 连接管理器使包可以连接到 ActiveX 数据对象 (ADO) 对象（如记录集）。 此连接管理器通常用于以 Microsoft Visual Basic 6.0 等语言的早期版本编写的自定义任务，或用于从属于使用 ADO 连接到数据源的现有应用程序的自定义任务。  
  
 将 ADO 连接管理器添加到包时， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时解析为 ADO 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到 `Connections` 包上的集合。 该连接管理器的 `ConnectionManagerType` 属性设置为 `ADO`。  
  
## <a name="troubleshooting-the-ado-connection-manager"></a>ADO 连接管理器故障排除  
 ADO 连接管理器在读取数据时，某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期数据类型将生成下表中显示的结果。  
  
|SQL Server 数据类型|结果|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|除非包使用参数化 SQL 命令，否则，包将失败。 若要使用参数化 SQL 命令，请在包中使用执行 SQL 任务。 有关详细信息，请参阅 [执行 SQL 任务](../control-flow/execute-sql-task.md) 和 [执行 SQL 任务中的参数和返回代码](../parameters-and-return-codes-in-the-execute-sql-task.md)。|  
|`datetime2`|ADO 连接管理器截断毫秒值。|  
  
> [!NOTE]  
>  有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和它们如何映射到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型的详细信息，请参阅[数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql) 和 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
## <a name="configuring-the-ado-connection-manager"></a>配置 ADO 连接管理器  
 可以使用下列方式配置 ADO 连接管理器：  
  
-   提供配置为满足选定访问接口要求的特定连接字符串。  
  
-   包括要连接到的数据源的名称（取决于访问接口）。  
  
-   为选定的访问接口提供相应的安全凭据。  
  
-   指示是否在运行时保留从连接管理器中创建的连接。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [配置 OLE DB 连接管理器](ole-db-connection-manager.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 连接](integration-services-ssis-connections.md)  
  
  
