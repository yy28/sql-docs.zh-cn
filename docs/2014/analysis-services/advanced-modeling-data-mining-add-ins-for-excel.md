---
title: 高级建模 （数据挖掘外接程序 excel） |Microsoft 文档
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining structures, creating
ms.assetid: 042270a3-6ec7-4b52-b2ba-2adb6c4740d5
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: de7eea9099b458a9f16e6928c1535dc4a03eb81a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017230"
---
# <a name="advanced-modeling-data-mining-add-ins-for-excel"></a>高级建模（Excel 数据挖掘外接程序）
  你可以使用**高级**建模选项可创建带参数的自定义数据挖掘结构和模型不同于通过向导创建的那些数据。 本节中介绍的两个向导可以帮助您创建全新的数据挖掘结构，以及可应用于现有数据挖掘结构的新挖掘模型。  
  
## <a name="create-mining-structure"></a>创建挖掘结构  
 ![挖掘结构创建按钮，数据挖掘功能区](media/dmc-createstruct.gif "创建挖掘结构按钮，数据挖掘功能区")  
  
 **创建挖掘结构向导**帮助你生成新的数据挖掘结构。 结构是从指定数据源提取的数据集合。  挖掘结构可以使用源中的新数据更新，但您在创建挖掘结构时需要定义数据类型和名称，以规定如何在分析中使用数据。  
  
 可以使用以下数据源生成结构：Excel 表、Excel 区域或已定义为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源视图的外部数据源中的任何数据。  
  
 对于每种结构，您都可以选择留出一些数据来用于测试和验证。 通过创建此*维持数据集*时设置您的数据源时，你可以确保基于该结构的所有模型都都能为测试中使用一致的数据集。  
  
 创建挖掘结构之后，可以添加多个挖掘模型来应用不同的分析方法。  
  
 有关如何使用**创建挖掘结构向导**，请参阅[创建挖掘结构&#40;SQL Server 数据挖掘外接程序&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)。  
  
## <a name="add-model-to-structure"></a>将模型添加到结构  
 ![将模型添加到结构按钮](media/dmc-addmodel.gif "到结构按钮添加模型")  
  
 在向结构中添加新的模型时，可以通过使用不同的算法或者不同的参数对数据进行分析。 如果要使用“数据挖掘客户端”工具中未公开的某种算法创建模型，此选项尤其有用。  
  
 您可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持的任意算法，例如：  
  
-   线性回归  
  
-   顺序分析和聚类分析  
  
-   嵌套数据集的关联分析  
  
 若要查看有哪些类型的挖掘结构可用，你可以浏览模型和结构存储在[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]通过单击**管理模型**或**浏览**。  
  
 您只能看到当前会话过程中创建的数据挖掘结构或保存到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的挖掘结构。  
  
 有关详细信息，请参阅[添加到结构的模型&#40;for Excel 的数据挖掘外接&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)。  
  
## <a name="see-also"></a>请参阅  
 [管理模型&#40;SQL Server 数据挖掘外接程序&#41;](manage-models-sql-server-data-mining-add-ins.md)   
 [浏览 Excel 中的模型&#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  