---
title: Excel 连接管理器 | Microsoft Docs
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 39c0937448194dba61eb20d5e1492c71a57bf80a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968065"
---
# <a name="excel-connection-manager"></a>Excel 连接管理器

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Excel 连接管理器使包可以连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 工作簿文件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所包含的 Excel 源和 Excel 目标使用 Excel 连接管理器。  
 
> [!IMPORTANT]
> 有关连接到 Excel 文件的详细信息，以及从 Excel 文件加载数据或将数据加载到 Excel 文件的限制和已知问题，请参阅[使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](../load-data-to-from-excel-with-ssis.md)。

 将 Excel 连接管理器添加到包时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时作为 Excel 连接进行解析的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包上的 **Connections** 集合。  
  
 该连接管理器的 **ConnectionManagerType** 属性设置为 **EXCEL**。  
  
## <a name="configure-the-excel-connection-manager"></a>配置 Excel 连接管理器  
 可以按照下列方式配置 Excel 连接管理器：  
  
-   指定 Excel 工作簿文件的路径。  
  
-   指定用于创建文件的 Excel 的版本。  
  
-   指示所选工作表或区域中的第一行是否包含列名称。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [Excel 连接管理器编辑器](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
## <a name="excel-connection-manager-editor"></a>Excel 连接管理器编辑器
  使用 **“Excel 连接管理器编辑器”** 对话框可以将连接添加到现有或新的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 工作簿文件。  
  
### <a name="options"></a>选项  
 **Excel 文件路径**  
 键入一个现有或新的 Excel 工作簿文件的路径和文件名。  
   
 **“浏览”**  
 使用“打开”对话框导航到 Excel 文件所在的文件夹或要创建新文件的文件夹  。  
  
 **Excel 版本**  
 指定用于创建文件的 Microsoft Excel 的版本。  
  
 **首行包含列名称**  
 指定所选工作表中的第一行数据是否包含列名称。 此选项的默认值为 **True**。  
  
## <a name="related-tasks"></a>Related Tasks  
[使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](../load-data-to-from-excel-with-ssis.md)  
[Excel 源](../data-flow/excel-source.md)  
[Excel 目标](../data-flow/excel-destination.md)
