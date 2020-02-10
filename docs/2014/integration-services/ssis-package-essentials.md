---
title: SSIS 包基础知识 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- package requirements
ms.assetid: b0c86c35-e3d3-4724-9a96-4087e9d74bf3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8cba1fb860d884b568fe132fc2b38ff50fbd480d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055419"
---
# <a name="ssis-package-essentials"></a>SSIS 包基本要素
  包是用于实现 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 功能以提取、转换和加载数据的对象。 可以通过使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 中的 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]设计器来创建包。 也可以通过运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导或 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 连接项目向导来创建包。 有关详细信息，请在 SSIS 设计器和[导入项目向导](../../2014/integration-services/import-project-wizard.md) [SQL Server Data Tools 中创建包](create-packages-in-sql-server-data-tools.md)。  
  
 基本包中包括以下元素：  
  
 **控制流元素**  
 此类必需的元素执行各种功能，提供结构以及控制元素运行的顺序。 主控制流元素是指任务、容器和优先约束。 包中必须至少有一个控制流元素。  
  
 有关详细信息，请参阅 [Control Flow](control-flow/control-flow.md)。  
  
 **数据流元素**  
 此类可选的元素可提取数据，修改数据以及将数据加载到数据源。 主数据流元素是指源、转换和目标。 包中不一定要包含数据流元素。  
  
 有关详细信息，请参阅 [Data Flow](data-flow/data-flow.md)。  
  
 有关如何创建基本包的示例，请参阅[第1课：创建项目和基本包](lesson-1-create-a-project-and-basic-package-with-ssis.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [在 SQL Server Data Tools 中创建包](create-packages-in-sql-server-data-tools.md)  
  
-   [在控制流中添加或删除任务或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
-   [设置任务或容器的属性](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
-   [在数据流中添加或删除组件](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
## <a name="related-content"></a>相关内容  
  
1.  MSDN.Microsoft.com 上的视频 [创建基本包（SQL Server 视频）](https://go.microsoft.com/fwlink/?LinkId=131023)  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 包](../../2014/integration-services/integration-services-ssis-packages.md)   
 [优先约束](control-flow/precedence-constraints.md)  
  
  
