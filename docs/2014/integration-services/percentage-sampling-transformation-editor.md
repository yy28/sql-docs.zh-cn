---
title: 百分比抽样转换编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- Percentage Sampling Transformation Editor
ms.assetid: 2c40d804-26a3-4d35-809b-bc923d83d451
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0366ecb08281a28d43bc98639bf4b11e60aea402
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66056719"
---
# <a name="percentage-sampling-transformation-editor"></a>百分比抽样转换编辑器
  可以使用 **“百分比抽样转换编辑器”** 对话框，使用指定的行百分比将部分输入拆分成样本。 此转换将输入分成两个单独的输出。  
  
 若要了解有关百分比抽样转换的详细信息，请参阅 [Percentage Sampling Transformation](data-flow/transformations/percentage-sampling-transformation.md)。  
  
## <a name="options"></a>选项  
 **行百分比**  
 指定输入中要用作样本的行百分比。  
  
 此属性的值可以使用属性表达式来指定。  
  
 **样本的输出名称**  
 为包含抽样行的输出提供唯一名称。 所提供的名称将显示在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中。  
  
 **未选中部分的输出名称**  
 为包含非抽样行的输出提供唯一名称。 所提供的名称将显示在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中。  
  
 **使用以下随机种子**  
 指定随机数生成器的抽样种子，转换将使用该种子来创建样本。 建议只在开发和测试过程中使用此选项。 如果未指定随机种子，转换将使用 Microsoft Windows 的时钟周期计数。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [行抽样转换](data-flow/transformations/row-sampling-transformation.md)  
  
  
