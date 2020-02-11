---
title: 创建测试集（数据挖掘向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.holdout.f1
ms.assetid: d0a44b59-ffbd-45fc-baa8-6b8046b1a2f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f0e4d1a384995c0c49c346102f8fddbcdf47f68
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086793"
---
# <a name="create-testing-set-data-mining-wizard"></a>创建测试集（数据挖掘向导）
  可以使用 **“创建测试集”** 页指定用于定型的数据量，以及为用作测试集而保留的数据量。 在创建挖掘结构时将数据分成定型集和测试集，可以更方便地评估以后创建的挖掘模型的准确性。  
  
 您可以将测试数据量指定为百分比，也可以指定一个数字来限定用于测试的事例的数量。 如果同时指定百分比和用于测试的事例的最大数量，则将同时使用这两个设置，测试数据集将包含较少的事例数。 默认情况下，30 % 的数据用于测试，70 % 的数据用于定型，没有最大测试事例数。  
  
 默认情况下， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 生成用于启动分区的数值种子。 此种子基于挖掘结构的名称。 如果希望即使在挖掘结构名称更改的情况下分区仍保持不变，则可以设置挖掘结构的 HoldoutSeed 属性，为种子指定一个值。 如果更改维持种子，则必须重新处理该结构。  
  
 如果以后要更改测试数据量或定型数据量，则可以使用 "**属性**" `HoldoutMaxCases`窗口`HoldoutMaxPercent`修改数据挖掘结构的和属性。 不过，进行更改后，必须重新处理挖掘结构及所有关联挖掘模型。 还存在下列限制：  
  
-   仅当数据挖掘结构存储在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]中时，才支持数据挖掘结构的分区。 的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]早期版本不支持缓存挖掘结构的分区信息。  
  
-   如果挖掘结构包含 Key Time 列（这是时序挖掘模型所必需的），则无法对挖掘结构进行分区。  
  
-   如果尝试预测的值存储在嵌套表中，则无法对数据进行分区。  
  
 **有关详细信息**，请[&#40;数据挖掘&#41;中的测试和验证](data-mining/testing-and-validation-data-mining.md)、[创建关系挖掘结构](data-mining/create-a-relational-mining-structure.md)、[数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
## <a name="options"></a>选项  
 **测试数据百分比**  
 单击向上箭头和向下箭头可以增大或减小用作测试数据的数据百分比，也可以在文本框中键入介于 0 到 100 之间的值。  
  
 **测试数据集中的最大事例数**  
 键入一个数字，以限制可用于测试的事例数。  
  
 如果指定的数字大于数据中的实际事例数，则将使用所有事例。  
  
 默认值为 NULL。 这表示没有限制。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘向导 F1 帮助 &#40;Analysis Services 数据挖掘&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [在数据挖掘向导 &#40;建议相关列&#41;](suggest-related-columns-data-mining-wizard.md)   
 [在数据挖掘向导 &#40;指定表类型&#41;](specify-table-types-data-mining-wizard.md)   
 [指定数据挖掘向导 &#40;列的内容和数据类型&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
