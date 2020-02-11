---
title: Excel 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 432d48bbe848d6f66e9f3dae5365abe10d8deb62
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833835"
---
# <a name="excel-connection-manager"></a>Excel 连接管理器
  Excel 连接管理器使包可以连接到现有的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 工作簿文件。 包含的 excel 源和 excel 目标[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 excel 连接管理器。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
 将 Excel 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时决定 Excel 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包上的 `Connections` 集合。  
  
 该连接管理器的 `ConnectionManagerType` 属性设置为 `EXCEL`。  
  
> [!NOTE]  
>  无法连接到受密码保护的 Excel 文件。  
  
## <a name="configuration-of-the-excel-connection-manager"></a>Excel 连接管理器的配置  
 可以按照下列方式配置 Excel 连接管理器：  
  
-   指定 Excel 工作簿文件的路径。  
  
-   指定用于创建文件的 Excel 的版本。  
  
-   指示所选工作表或范围中的第一行被访问数据是否包含列名称。  
  
 如果 Excel 源使用 Excel 连接管理器，则被提取的数据将附带列名称。 如果 Excel 目标使用它，则列名称包括在被写入的数据中。  
  
 Excel 连接管理器使用 Jet [!INCLUDE[msCoName](../../includes/msconame-md.md)] 4.0 的 OLE DB 提供程序及其支持的 excel ISAM （索引顺序访问方法）驱动程序来连接 excel 数据源并对其进行读取和写入。 有关与 Excel 源和 Excel 目标结合使用时，此提供程序和驱动程序的行为的详细信息，请参阅[Excel 源](../data-flow/excel-source.md)和[excel 目标](../data-flow/excel-destination.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [Excel 连接管理器编辑器](../excel-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
 有关循环遍历 Excel 文件中的某个组的信息，请参阅 [使用 Foreach 循环容器，循环遍历 Excel 文件和表](../control-flow/foreach-loop-container.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [使用 Foreach 循环容器，循环遍历 Excel 文件和表](../control-flow/foreach-loop-container.md)  
  
-   [使用 SQL Server Integration Services (SSIS) 从 Excel 导入数据或将数据导出到 Excel](../load-data-to-from-excel-with-ssis.md)
  
  
