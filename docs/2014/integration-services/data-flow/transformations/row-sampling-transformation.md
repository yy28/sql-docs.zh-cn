---
title: 行抽样转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rowsamplingtrans.f1
helpviewer_keywords:
- sampling seeds [Integration Services]
- random seeds
- random sampling
- sample data sets [Integration Services]
- Row Sampling transformation
- packages [Integration Services], samples
- datasets [Integration Services], sample
ms.assetid: b6caafd3-30b2-4368-82af-a44611d4cd39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 954e8b2a2f36ccab1cff97174089560913291074
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770388"
---
# <a name="row-sampling-transformation"></a>行抽样转换
  行抽样转换用于获取输入数据集的随机选择子集。 您可以指定输出样本的准确大小，并指定随机数生成器的种子。  
  
 随机抽样有许多应用场合。 例如，如果公司需要以抽彩给奖法随机选择 50 名雇员接受奖励，则可对雇员数据库使用行随机抽样转换来生成准确数目的获奖者。  
  
 在包开发过程中，也可以使用行抽样转换来创建一个小但具有代表性的数据集。 这样，您就可以使用很有代表性的数据来测试包执行和数据转换，而且这种测试更加快捷，因为它使用的是随机样本而不是全部数据集。 因为测试包使用的样本数据集始终是同一大小，所以使用样本子集还可以轻松地识别出包中的性能问题。  
  
 此转换类似于百分比抽样转换，后者通过选择输入行的百分比来创建样本数据集。 请参阅 [Percentage Sampling Transformation](percentage-sampling-transformation.md)。  
  
## <a name="configuring-the-row-sampling-transformation"></a>配置行抽样转换  
 行抽样转换通过选择指定数目的转换输入行来创建样本数据集。 因为从转换输入中选择的行是随机的，因此结果样本可以代表输入。 还可以指定随机数生成器使用的种子来影响转换选择行的方式。  
  
 在同一转换输入上使用相同的随机种子将始终创建相同的样本输出。 如果没有指定种子，转换将使用操作系统的时钟周期数来创建随机数。 因此，可使用测试期间使用的种子来验证包开发和测试期间的转换结果，然后在包进入生产阶段时改用随机种子。  
  
 行抽样转换包括 `SamplingValue` 自定义属性。 加载包时，可以通过属性表达式更新此属性。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../expressions/integration-services-ssis-expressions.md)、[在包中使用属性表达式](../../expressions/use-property-expressions-in-packages.md)和[转换自定义属性](transformation-custom-properties.md)。  
  
 此转换有一个输入和两个输出。 它没有错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在“百分比抽样转换编辑器”  对话框中设置的属性的详细信息，请参阅[行抽样转换编辑器（“抽样”页）](../../row-sampling-transformation-editor-sampling-page.md)。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [转换自定义属性](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)  
  
  
