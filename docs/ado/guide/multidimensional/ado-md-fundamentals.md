---
description: ADO MD 基础知识
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fec7d924003df2a0c0c20b5ca2b0de9162cfd1c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452439"
---
# <a name="ado-md-fundamentals"></a>ADO MD 基础知识
Microsoft® ActiveX®数据对象 (多维)  (ADO MD) 允许从 Microsoft Visual Basic® Microsoft Visual C++®等语言轻松访问多维数据。 ADO MD 将 Microsoft ActiveX®数据对象扩展 (ADO) ，以包含特定于多维数据的对象，例如 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) 和 [单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 对象。 使用 ADO MD 可以浏览多维架构、查询多维数据集和检索结果。  
  
 与 ADO 一样，ADO MD 使用底层 OLE DB 提供程序来获取对数据的访问权限。 若要使用 ADO MD，提供程序必须是多维数据提供程序 (MDP) ，如 OLAP 规范的 OLE DB 所定义。 MDP 在多维视图而不是表格视图中呈现数据，表格视图是表格数据访问接口 (TDP) 显示数据的方式。 有关提供程序支持的特定语法和行为的详细信息，请参阅 OLAP OLE DB 提供程序的文档。  
  
 本文档假定你了解 Visual Basic 的编程语言和 ADO 和 OLAP 的一般知识。 有关详细信息，请参阅 [ADO 程序员指南](../../../ado/guide/ado-programmer-s-guide.md) 和 [OLE DB，了解联机分析处理 (OLAP) ](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx)。  
  
 本部分包含以下主题。  
  
-   [多维架构和数据的概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [使用 ADO 与 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [使用 ADO MD 进行编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO 程序员指南](../../../ado/guide/ado-programmer-s-guide.md)   
 [数据定义语言和安全性的 ADO 扩展 (ADOX) ](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [多维架构和数据的概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [用 ADO MD 进行编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 与 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
