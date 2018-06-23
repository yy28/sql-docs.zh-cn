---
title: 行抽样转换编辑器 （抽样页） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql12.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- Row Sampling Transformation Editor
ms.assetid: 544c7709-6de0-4c08-bda3-759985be9a05
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0d17eb947e7291eaf3f5273cc1f1f21d11b0f307
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014325"
---
# <a name="row-sampling-transformation-editor-sampling-page"></a>行抽样转换编辑器（“抽样”页）
  可以使用 **“行抽样转换编辑器”** 对话框，使用指定行数将部分输入拆分成样本。 此转换将输入分成两个单独的输出。  
  
 若要了解有关行抽样转换的详细信息，请参阅 [Row Sampling Transformation](data-flow/transformations/row-sampling-transformation.md)。  
  
## <a name="options"></a>“常规”  
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
  
  