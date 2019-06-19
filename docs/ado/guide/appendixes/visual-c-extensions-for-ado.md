---
title: VisualC++的 ADO 扩展 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions for ADO
ms.assetid: 2952ece0-7217-4448-bb09-f6b64f43b7e2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ccd783bdb7bf266bfdc83c3a02520345d707ceea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702630"
---
# <a name="visual-c-extensions-for-ado"></a>ADO 的 Visual C++ 扩展
编程 ADO 与视觉对象的首选的方法C++使用 **#import**指令，如中所述[Microsoft Visual C++ ADO 编程](../../../ado/guide/appendixes/visual-c-ado-programming.md)。 但是，早期版本的 ADO 使用视觉对象的编程的另一种方法随一起提供C++： 视觉对象C++扩展。 本部分介绍此功能对于那些必须维护视觉对象C++扩展的代码，但新的 ADO 代码应使用编写 #**导入**。

 最麻烦的作业视觉对象中的一个C++编程人员人脸使用 ADO 检索数据将数据转换时返回到 VARIANT 数据类型为C++数据类型，然后将转换后的数据存储在类或结构。 除了繁琐外，检索C++通过 VARIANT 数据类型的数据会降低性能。

 ADO 提供了接口，支持数据检索至本机 C /C++数据类型而无需通过变体，并还提供了预处理器宏，可以简化使用接口。 结果是一个灵活的工具，更易于使用，并且可以提供最佳性能。

 常见的 C /C++客户端的方案是将绑定中的记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)到 C /C++结构或类包含本机 C /C++类型。 变体时，这涉及到从变体编写转换代码到 C /C++的本机类型。 视觉对象C++针对 ADO 扩展使此方案中更容易的视觉对象C++程序员。

 请参阅以下主题，了解有关视觉对象的详细信息C++ADO 的扩展。

-   [使用视觉对象C++的 ADO 扩展](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual C++ 扩展标头](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [ADO 使用视觉对象C++扩展插件示例](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>请参阅
 [ADO 视觉对象C++COM 的语法索引](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [VisualC++扩展示例](../../../ado/guide/appendixes/visual-c-extensions-example.md)[使用视觉对象C++扩展](../../../ado/guide/appendixes/using-visual-c-extensions.md) [VisualC++扩展标头](../../../ado/guide/appendixes/visual-c-extensions-header.md)
