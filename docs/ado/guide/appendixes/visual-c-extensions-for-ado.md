---
title: ADO 的 visual c + + 扩展 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
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
manager: craigg
ms.openlocfilehash: ca21e976783a10a738488762e382982e4fd8fd8a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747675"
---
# <a name="visual-c-extensions"></a>Visual c + + 扩展
使用 Visual c + + ADO 编程的首选的方法使用 **#import**指令，如中所述[Microsoft Visual c + + ADO 编程](../../../ado/guide/appendixes/visual-c-ado-programming.md)。 但是，早期版本的 ADO 随使用 Visual c + + 编程的另一种方法： Visual c + + 扩展。 本部分介绍此功能对于那些必须维护 Visual c + + 扩展的代码，但应使用 # 编写新的 ADO 代码**导入**。

 一个最乏味作业 Visual c + + 编程人员所面临的当使用 ADO 检索数据将转换成 c + + 数据类型，返回为 VARIANT 数据类型，然后将转换后的数据存储在类或结构数据。 除了繁琐外，检索通过 VARIANT 数据类型的 c + + 数据会降低性能。

 ADO 提供到本机 C/c + + 数据类型支持检索数据，而无需通过变体，一个接口，还提供预处理器宏，可以简化使用接口。 结果是一个灵活的工具，更易于使用，并且可以提供最佳性能。

 一种常见的 C/c + + 客户端方案是将绑定中的记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)到 C/c + + 结构或类包含本机 C/c + + 类型。 变体时，这涉及到 C/c + + 本机类型从 VARIANT 编写转换代码。 使此方案中的 Visual c + + 程序员更容易针对 ADO 的 Visual c + + 扩展。

 请参阅以下主题，了解有关 ADO 的 Visual c + + 扩展的详细信息。

-   [使用 ADO 的 Visual c + + 扩展](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual C++ 扩展标头](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [ADO 与 Visual c + + 扩展示例](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>请参阅
 [Visual c + + 语法索引 COM 的 ADO](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [Visual c + + 扩展示例](../../../ado/guide/appendixes/visual-c-extensions-example.md)[使用 Visual c + + 扩展](../../../ado/guide/appendixes/using-visual-c-extensions.md) [Visual c + + 扩展标头](../../../ado/guide/appendixes/visual-c-extensions-header.md)
