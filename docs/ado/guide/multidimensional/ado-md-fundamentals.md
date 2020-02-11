---
title: ADO MD 基础 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 690c7b58c336596485b9ade77f0c02928853cd2d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923205"
---
# <a name="ado-md-fundamentals"></a>ADO MD 基础知识
Microsoft® ActiveX®数据对象（多维）（ADO MD）提供了从 Microsoft Visual Basic® Microsoft Visual C++®等语言轻松访问多维数据的权限。 ADO MD 扩展 Microsoft ActiveX®数据对象（ADO）以包括特定于多维数据的对象，例如[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)和[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象。 使用 ADO MD 可以浏览多维架构、查询多维数据集和检索结果。  
  
 与 ADO 一样，ADO MD 使用底层 OLE DB 提供程序来获取对数据的访问权限。 若要使用 ADO MD，提供程序必须是由 OLAP 规范的 OLE DB 定义的多维数据提供程序（MDP）。 MDP 在多维视图而不是表格视图中呈现数据，表格视图是表格数据访问接口（TDP）显示数据的方式。 有关提供程序支持的特定语法和行为的详细信息，请参阅 OLAP OLE DB 提供程序的文档。  
  
 本文档假定你了解 Visual Basic 的编程语言和 ADO 和 OLAP 的一般知识。 有关详细信息，请参阅[用于联机分析处理（OLAP）](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx)的[ADO 程序员指南](../../../ado/guide/ado-programmer-s-guide.md)和 OLE DB。  
  
 本部分包含下列主题。  
  
-   [多维架构和数据的概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [使用 ADO 与 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [使用 ADO MD 进行编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO 程序员指南](../../../ado/guide/ado-programmer-s-guide.md)   
 [数据定义语言和安全性（ADOX）的 ADO 扩展](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [多维架构和数据的概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [用 ADO MD 进行编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 与 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
