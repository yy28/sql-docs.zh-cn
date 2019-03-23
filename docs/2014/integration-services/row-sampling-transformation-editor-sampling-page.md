---
title: 行抽样转换编辑器 （抽样页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql12.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- Row Sampling Transformation Editor
ms.assetid: 544c7709-6de0-4c08-bda3-759985be9a05
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 13117cd751b093497b2faaacd42ff9558fac654d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392025"
---
# <a name="row-sampling-transformation-editor-sampling-page"></a>行抽样转换编辑器（“抽样”页）
  可以使用 **“行抽样转换编辑器”** 对话框，使用指定行数将部分输入拆分成样本。 此转换将输入分成两个单独的输出。  
  
 若要了解有关行抽样转换的详细信息，请参阅 [Row Sampling Transformation](data-flow/transformations/row-sampling-transformation.md)。  
  
## <a name="options"></a>选项  
 **行数**  
 指定输入中要用作样本的行数。  
  
 此属性的值可以使用属性表达式来指定。  
  
 **样本的输出名称**  
 为包含抽样行的输出提供唯一名称。 所提供的名称将在 SSIS 设计器中显示。  
  
 **未选中部分的输出名称**  
 为包含非抽样行的输出提供唯一名称。 所提供的名称将在 SSIS 设计器中显示。  
  
 **使用以下随机种子**  
 指定随机数生成器的抽样种子，转换将使用该种子来创建样本。 建议只在开发和测试过程中使用此选项。 如果未指定随机种子，则转换将使用 Microsoft Windows 的时钟周期计数作为种子。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [百分比抽样转换](data-flow/transformations/percentage-sampling-transformation.md)  
  
  
