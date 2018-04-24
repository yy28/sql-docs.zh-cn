---
title: ADO MD 基础知识 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8160377b66ba6a781a92ef772795782eaa455478
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="ado-md-fundamentals"></a>ADO MD 基础知识
Microsoft® ActiveX® 数据对象 （多维） (ADO MD) 轻松访问通过提供对多维数据等 Microsoft Visual Basic®，语言 Microsoft Visual C++®。 ADO MD 扩展 Microsoft ActiveX® 数据对象 (ADO) 要包括特定于多维数据的对象，如[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)和[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象。 使用 ADO MD 中，您可以浏览多维架构、 查询多维数据集，并检索结果。  
  
 ADO，如 ADO MD 使用基础的 OLE DB 提供程序对数据进行访问。 若要使用 ADO MD，提供程序必须是多维数据提供程序 (MDP)，因为 OLE DB for OLAP 规范所定义。 MDP 显示这是表格数据提供程序 (TDP) 在呈现数据的方式而不是表格视图的多维视图中的数据。 请参阅您有关的特定语法和行为你提供程序支持的详细信息的 OLAP OLE DB 提供程序文档。  
  
 本文档假定 Visual Basic 编程语言的应用知识和 ADO 和 OLAP 的常规知识。 有关详细信息，请参阅[ADO 程序员指南](../../../ado/guide/ado-programmer-s-guide.md)和[OLE DB 的联机分析处理 (OLAP)](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx)。  
  
 本部分包含以下主题。  
  
-   [多维架构和数据的概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [使用 ADO 与 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [使用 ADO MD 进行编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO 程序员指南](../../../ado/guide/ado-programmer-s-guide.md)   
 [适用于数据定义语言和安全 (ADOX) 的 ADO 扩展](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [多维架构和数据概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 的 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
