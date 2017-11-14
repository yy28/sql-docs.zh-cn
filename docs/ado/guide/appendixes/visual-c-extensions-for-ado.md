---
title: "ADO 的 visual c + + 扩展 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions for ADO
ms.assetid: 2952ece0-7217-4448-bb09-f6b64f43b7e2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fbc17b15d552f9b7afeeb4841febdd7d08e54808
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="visual-c-extensions"></a>Visual c + + 扩展
编程 Visual c + + 的 ADO 的首选的方法使用**#import**指令中, 所述[Microsoft Visual c + + ADO 编程](../../../ado/guide/appendixes/visual-c-ado-programming.md)。 但是，早期版本的 ADO 附带使用 Visual c + + 编程的另一种方法： Visual c + + 扩展。 本部分介绍此功能的用户的用户必须维护 Visual c + + 扩展代码，但应使用 # 编写新的 ADO 代码**导入**。

 一个最繁琐作业 Visual c + + 程序员表面时检索数据用 ADO 将转换成 c + + 数据类型，作为 VARIANT 数据类型返回，并且然后将转换的数据存储在类或结构中的数据。 除了繁琐外，c + + 通过检索数据 VARIANT 数据类型会降低性能。

 ADO 提供了为本机 C/c + + 数据类型支持检索数据，而无需通过一个变量，一个接口，并提供简化使用接口的预处理器宏。 结果是一个灵活的工具，可以更轻松地使用具有卓越性能。

 一个常见的 C/c + + 客户端方案是将绑定中的记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)到 C/c + + 结构或类包含本机 C/c + + 类型。 时经过变体，这涉及到 C/c + + 本机类型从 VARIANT 编写转换代码。 使这种情况下为 Visual c + + 程序员更容易面向 ADO 的 Visual c + + 扩展。

 请参阅以下主题以了解有关 ADO 的 Visual c + + 扩展的详细信息。

-   [使用 ADO 的 Visual c + + 扩展](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Visual c + + 扩展标头](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [ADO 与 Visual c + + 扩展示例](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>另请参阅
 [有关 COM 的 Visual c + + 语法索引的 ADO](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [Visual c + + 扩展示例](../../../ado/guide/appendixes/visual-c-extensions-example.md)[使用 Visual c + + 扩展](../../../ado/guide/appendixes/using-visual-c-extensions.md) [Visual c + + 扩展标头](../../../ado/guide/appendixes/visual-c-extensions-header.md)

