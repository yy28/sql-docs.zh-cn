---
title: 错误配置 （挖掘结构对话框） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.miningstructuredialog.general.f1
ms.assetid: d9aa028b-bad9-49c7-a81c-c2150e4dd481
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 73c3627f3861b978a9e539943bcb65777b2f36b1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257403"
---
# <a name="error-configuration-mining-structure-dialog-box-analysis-services---multidimensional-data"></a>错误配置（“挖掘结构”对话框）（Analysis Services - 多维数据）
  可以使用 **SQL Server Management Studio** 中的 **“挖掘结构属性”** 对话框的 **“错误配置”** 页，设置 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中的挖掘结构的错误配置属性。  
  
## <a name="options"></a>“常规”  
 **使用默认错误配置**  
 选择此选项可以在处理操作中使用对象的默认错误配置。  
  
 **键错误操作**  
 选择以下操作之一，以便在处理过程中遇到找不到的新键时执行：  
  
-   **“转换为未知”** 将记录信息聚合到未知成员中。  
  
-   **“放弃记录”** 将排除记录信息，以免与对象一起处理。  
  
 **忽略错误计数**  
 单击此项可忽略处理过程中发生的任何错误。  
  
 **出错时停止**  
 单击此项可在出错时停止处理。 此选项将启用 **“错误数”** 和 **“出错时要执行的操作”** 选项。  
  
 **错误数**  
 键入处理停止前忽略的错误数。  
  
 **出错时要执行的操作**  
 选择以下操作之一，以便在错误数超出“错误数”中的值时执行该操作：  
  
-   **“停止处理”** 将结束处理操作。  
  
-   **“停止日志记录”** 将停止记录错误，但继续处理操作。  
  
 **找不到键**  
 指定以下操作之一，以便在处理对象的过程中找不到键时执行该操作：  
  
-   **忽略错误** ，将忽略该错误  
  
-   **报告并继续** ，报告该错误并继续处理操作  
  
-   **“报告并停止”** ，报告该错误并停止处理操作。  
  
 **重复键**  
 指定以下操作之一，以便在处理对象的过程中发现重复键时执行该操作：  
  
-   **忽略错误** ，将忽略该错误  
  
-   **报告并继续** ，报告该错误并继续处理操作  
  
-   **“报告并停止”** ，报告该错误并停止处理操作。  
  
 **空键转换为未知键**  
 指定以下操作之一，以便在处理对象的过程中向未知成员添加 Null 成员键时执行该操作：  
  
-   **忽略错误** ，将忽略该错误  
  
-   **报告并继续** ，报告该错误并继续处理操作  
  
-   **“报告并停止”** ，报告该错误并停止处理操作。  
  
 **不允许空键**  
 指定以下操作之一，以便在处理对象的过程中发现不允许的 Null 键时执行该操作：  
  
-   **忽略错误** ，将忽略该错误  
  
-   **报告并继续** ，报告该错误并继续处理操作  
  
-   **“报告并停止”** ，报告该错误并停止处理操作。  
  
 **错误日志路径**  
 键入错误日志文件的完整路径和文件名。  
  
## <a name="see-also"></a>请参阅  
 [挖掘结构属性对话框&#40;Analysis Services-数据挖掘&#41;](mining-structure-properties-dialog-analysis-services-data-mining.md)   
 [常规&#40;挖掘结构对话框的&#41; &#40;Analysis Services-数据挖掘&#41;](general-mining-structure-dialog-box-analysis-services-data-mining.md)  
  
  
