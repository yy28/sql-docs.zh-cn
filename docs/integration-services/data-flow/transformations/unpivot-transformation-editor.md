---
title: "逆透视转换编辑器 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.unpivottransformation.f1
helpviewer_keywords:
- Unpivot Transformation Editor
ms.assetid: 72a36ef0-4070-4f6c-9c74-0720109617dd
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 186c56005a040d9a86f4d5dcb08599e2d650cb01
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="unpivot-transformation-editor"></a>“逆透视转换编辑器”
  可以使用 **“逆透视转换编辑器”** 对话框，选择要透视到行中的列以及指定数据列和新的透视值输出列。  
  
> [!NOTE]  
>  本主题围绕 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md) 中所述的“逆透视”应用场景，举例说明各选项的使用方法。  
  
 若要了解有关逆透视转换的详细信息，请参阅 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)。  
  
## <a name="options"></a>选项  
 **可用输入列**  
 使用复选框指定要透视到行中的列。  
  
 **名称**  
 查看可用输入列的名称。  
  
 **传递**  
 指示是否在逆透视的输出中包括该列。  
  
 **输入列**  
 从每行的可用输入列的列表中选择。 通过选中 **“可用输入列”** 表中的复选框来选择列。  
  
 在 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)所述的“逆透视”应用场景中，输入列为 **Ham**, **Soda**, **Milk**, **Beer**和 **Chips** 列。  
  
 **目标列**  
 提供数据列的名称。  
  
 在 [逆透视转换](../../../integration-services/data-flow/transformations/unpivot-transformation.md)所述的“逆透视”应用场景中，目标列为数量 (**Qty**) 列。  
  
 **透视键值**  
 提供透视值的名称。 默认值为输入列的名称；不过，您也可以任选一个唯一的描述性名称。  
  
 此属性的值可以使用属性表达式来指定。  
  
 在 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)所述的“逆透视”应用场景中，透视值将显示为由 **“透视键值列名”** 选项指定的新 Product 列中的文本值，即 **Ham**, **Soda**, **Milk**, **Beer**和 **Chips**。  
  
 **“透视键值列名”**  
 提供透视值列的名称。 默认名称为“Pivot Key Value”；不过，您也可以任选一个唯一的描述性名称。  
  
 在 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)所述的“逆透视”应用场景中，“透视键值列名”为 **Product** ，并指定新的 **Product** 列， **Ham**, **Soda**, **Milk**, **Beer**和 **Chips** 列将逆向透视到该列。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)   
 [透视转换](../../../integration-services/data-flow/transformations/pivot-transformation.md)  
  
  
