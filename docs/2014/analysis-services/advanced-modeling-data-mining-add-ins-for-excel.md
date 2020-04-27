---
title: 高级建模（Excel 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures, creating
ms.assetid: 042270a3-6ec7-4b52-b2ba-2adb6c4740d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 669fa1fcd9e4802a4d4102120a373dd615741017
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062739"
---
# <a name="advanced-modeling-data-mining-add-ins-for-excel"></a>高级建模（Excel 数据挖掘外接程序）
  您可以使用**高级**数据建模选项来创建自定义数据挖掘结构和模型，其中的参数不同于向导创建的参数。 本节中介绍的两个向导可以帮助您创建全新的数据挖掘结构，以及可应用于现有数据挖掘结构的新挖掘模型。  
  
## <a name="create-mining-structure"></a>创建挖掘结构  
 ![“数据挖掘”功能区中的“创建挖掘结构”按钮](media/dmc-createstruct.gif "“数据挖掘”功能区中的“创建挖掘结构”按钮")  
  
 **创建挖掘结构向导**可帮助您生成新的数据挖掘结构。 结构是从指定数据源提取的数据集合。  挖掘结构可以使用源中的新数据更新，但您在创建挖掘结构时需要定义数据类型和名称，以规定如何在分析中使用数据。  
  
 可以使用以下数据源生成结构：Excel 表、Excel 区域或已定义为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源视图的外部数据源中的任何数据。  
  
 对于每种结构，您都可以选择留出一些数据来用于测试和验证。 通过在设置数据源时创建此*维持数据集*，可以确保所有基于该结构的模型都能够使用一致的数据集进行测试。  
  
 创建挖掘结构之后，可以添加多个挖掘模型来应用不同的分析方法。  
  
 有关如何使用**创建挖掘结构向导**的详细信息，请参阅[创建挖掘结构 &#40;SQL Server 数据挖掘外接程序&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)。  
  
## <a name="add-model-to-structure"></a>将模型添加到结构  
 ![“将模型添加到结构”按钮](media/dmc-addmodel.gif "“将模型添加到结构”按钮")  
  
 在向结构中添加新的模型时，可以通过使用不同的算法或者不同的参数对数据进行分析。 如果要使用“数据挖掘客户端”工具中未公开的某种算法创建模型，此选项尤其有用。  
  
 您可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持的任意算法，例如：  
  
-   线性回归  
  
-   顺序分析和聚类分析  
  
-   嵌套数据集的关联分析  
  
 若要查看可用的挖掘结构类型，可以通过单击 " [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] **管理模型**" 或 "**浏览**" 来浏览中存储的模型和结构。  
  
 您只能看到当前会话过程中创建的数据挖掘结构或保存到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的挖掘结构。  
  
 有关详细信息，请参阅[将模型添加到 &#40;用于 Excel 的数据挖掘外接程序&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)。  
  
## <a name="see-also"></a>另请参阅  
 [管理 &#40;SQL Server 数据挖掘外接程序的模型&#41;](manage-models-sql-server-data-mining-add-ins.md)   
 [在 Excel 中浏览模型 &#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
