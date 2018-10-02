---
title: Union All 转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.unionalltrans.f1
- sql13.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4fb378c8ec2021e856c654f57844de1d36a67746
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710135"
---
# <a name="union-all-transformation"></a>Union All 转换
  Union All 转换将多个输入组合到一个输出中。 例如，可将来自五个不同平面文件源的输出输入到 Union All 转换并将其组合到一个输出中。  
  
## <a name="inputs-and-outputs"></a>输入和输出  
 转换输入是一个接一个地添加到转换输出中的；不对行进行重新排序。 如果包需要排序的输出，则应使用合并转换而不是 Union All 转换。  
  
 连接到 Union All 转换的第一个输入是转换从中创建转换输出的输入。 随后连接到转换的输入中的列将会被映射到转换输出中的列。  
  
 若要合并输入，可将输入中的列映射到输出中的列。 每个输出列至少要有一个输入中的列与其映射。 两列间的映射要求各列的元数据相匹配。 例如，映射列必须具有相同的数据类型。  
  
 如果映射列包含字符串数据，并且输出列的长度比输入列短，则输出列长度会自动增加以便包含输入列。 未映射到输出列的输入列在输出列中被设置为空值。  
  
 此转换具有多个输入和一个输出。 它不支持错误输出。  
  
## <a name="configuration-of-the-union-all-transformation"></a>Union All 转换的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以编程方式设置的属性的详细信息，请参阅 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)。  
  
 有关如何设置属性的详细信息，请单击下列主题之一：  
  
-   [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="union-all-transformation-editor"></a>Union All 转换编辑器
  可以使用 **“Union All 转换编辑器”** 对话框，将多个输入行集合并到单个输出行集中。 通过在数据流中包含 Union All 转换，可以从多个数据流合并数据、通过嵌套 Union All 转换来创建复杂数据集、以及在更正数据中的错误之后重新合并行。  
  
### <a name="options"></a>选项  
 **输出列的名称**  
 为每一列键入一个别名。 默认值为第一个（引用）输入中输入列的名称；不过，您也可以任选一个唯一的描述性名称。  
  
 **Union All 输入 1**  
 从第一个（引用）输入中可用输入列的列表中选择。 映射的列的元数据必须匹配。  
  
 **Union All 输入 n**  
 从第二个或其他输入中可用输入列的列表中选择。 映射的列的元数据必须匹配。  
  
## <a name="related-tasks"></a>Related Tasks  
 [通过使用 Union All 转换来合并数据](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)  
  
  
