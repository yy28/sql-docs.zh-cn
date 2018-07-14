---
title: Excel 连接管理器 | Microsoft Docs
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
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 81dc5d87384613ba742986715e876a0b9bc809f0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187124"
---
# <a name="excel-connection-manager"></a>Excel 连接管理器
  Excel 连接管理器使包可以连接到现有的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 工作簿文件。 Excel 源和 Excel 目标的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]包括使用 Excel 连接管理器。  
  
 将 Excel 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时决定 Excel 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包上的 `Connections` 集合。  
  
 `ConnectionManagerType`连接管理器属性设置为`EXCEL`。  
  
> [!NOTE]  
>  无法连接到受密码保护的 Excel 文件。  
  
## <a name="configuration-of-the-excel-connection-manager"></a>Excel 连接管理器的配置  
 可以按照下列方式配置 Excel 连接管理器：  
  
-   指定 Excel 工作簿文件的路径。  
  
-   指定用于创建文件的 Excel 的版本。  
  
-   指示所选工作表或范围中的第一行被访问数据是否包含列名称。  
  
 如果 Excel 源使用 Excel 连接管理器，则被提取的数据将附带列名称。 如果 Excel 目标使用它，则列名称包括在被写入的数据中。  
  
 Excel 连接管理器使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]OLE DB Provider for Jet 4.0 及其支持的 Excel ISAM （索引顺序存取方法） 驱动程序来连接和读取并写入到 Excel 数据源的数据。 此提供程序和驱动程序在用于 Excel 源和 Excel 目标时的行为的详细信息，请参阅[Excel 源](../data-flow/excel-source.md)并[Excel 目标](../data-flow/excel-destination.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [Excel 连接管理器编辑器](../excel-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>并[连接以编程方式添加](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
 有关循环遍历 Excel 文件中的某个组的信息，请参阅 [使用 Foreach 循环容器，循环遍历 Excel 文件和表](../control-flow/foreach-loop-container.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [使用 Foreach 循环容器循环遍历 Excel 文件和表](../control-flow/foreach-loop-container.md)  
  
-   [使用 SQL Server Integration Services (SSIS) 将数据导入 Excel 或从 Excel 导出数据](../load-data-to-from-excel-with-ssis.md)
  
  
