---
title: ADO 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c6278b15b3e99808a015496dfa15b7b4b48b8724
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128806"
---
# <a name="ado-connection-manager"></a>ADO 连接管理器
  ADO 连接管理器使包可以连接到 ActiveX 数据对象 (ADO) 对象（如记录集）。 此连接管理器通常用于以 Microsoft Visual Basic 6.0 等语言的早期版本编写的自定义任务，或用于从属于使用 ADO 连接到数据源的现有应用程序的自定义任务。  
  
 当将 ADO 连接管理器添加到包， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建的连接设置连接管理器属性，并将连接管理器添加到将解析为在运行时的ADO连接管理器`Connections`上包的集合。 `ConnectionManagerType`的连接管理器的属性设置为`ADO`。  
  
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
  
 有关以编程方式配置连接管理器的信息，请参阅<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>和[添加连接以编程方式](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services &#40;SSIS&#41;连接](integration-services-ssis-connections.md)  
  
  
