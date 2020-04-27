---
title: 逆透视转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottrans.f1
helpviewer_keywords:
- Unpivot transformation
- more normalized data set [Integration Services]
- normalized data [Integration Services]
- datasets [Integration Services], normalized data
ms.assetid: f635c64b-a9c5-4f11-9c40-9cd9d5298c5d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 98a8476ef317a0ddfa6f7fc27c0c9572ed12817a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62770171"
---
# <a name="unpivot-transformation"></a>逆透视转换
  逆透视转换将来自单个记录中多个列的值扩展为单个列中具有同样值的多个记录，使得非规范的数据集成为较规范的版本。 例如，每个客户在列出客户名的数据集中各占一行，在该行的各列中显示购买的产品和数量。 逆透视转换将数据集规范之后，客户购买的每种产品在该数据集中各占一行。  
  
 下面的关系图显示对 Product 列逆透视数据之前的数据集。  
  
 ![逆透视后的数据集](../../media/mw-dts-18.gif "逆透视后的数据集")  
  
 下面的关系图显示对 Product 列逆透视数据之后的数据集。  
  
 ![逆透视前的数据集](../../media/mw-dts-17.gif "逆透视前的数据集")  
  
 在某些情况下，逆透视结果可能包含具有意外值的行。 例如，如果关系图中显示的要逆透视的示例数据在 Fred 的所有 Qty 列中都具有空值，则输出将只包括 Fred 的一行，而非五行。 Qty 列将为空或包含零，具体取决于列数据类型。  
  
## <a name="configuration-of-the-unpivot-transformation"></a>配置逆透视转换  
 逆透视转换包括 `PivotKeyValue` 自定义属性。 加载包时，可以通过属性表达式更新此属性。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../expressions/integration-services-ssis-expressions.md)、[在包中使用属性表达式](../../expressions/use-property-expressions-in-packages.md)和[转换自定义属性](transformation-custom-properties.md)。  
  
 此转换有一个输入和一个输出。 它没有错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“逆透视转换编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [“逆透视转换编辑器”](../../unpivot-transformation-editor.md)  
  
 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)。  
  
  
