---
title: "使用 ADO 的 ADO MD |Microsoft 文档"
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
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 38df55c27ced6e0a7b32c321e2b3968bedb73aa1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-ado-with-ado-md"></a>使用 ADO 的 ADO MD
ADO 和 ADO MD 是相关但独立的对象模型。 ADO 提供的对象用于连接到数据源、 执行命令、 检索表格数据和架构以表格格式的元数据和查看提供程序错误的信息。 ADO MD 提供用于检索多维数据和查看多维架构元数据的对象。  
  
 当使用 MDP 时，你可以选择使用 ADO、 ADO MD 和 / 或你的应用程序。 通过引用您的项目中的这两个库，你将具有完全访问权限 MDP 提供的功能。  
  
 它会经常用到使用者来获取多维数据集的平展、 表格视图。 你可以执行此操作通过使用 ADO[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 指定的源你[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)作为***源***参数[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**记录集**，而不是作为的源ADO MD**单元集**。  
  
 它还可查看架构元数据中的表格的视图，而不是对象的层次结构。 ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象使用户可以打开**记录集**包含架构信息。 ***QueryType***参数**OpenSchema**方法具有多个[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)与 Mdp 特别相关的值。 其值如下所示：  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 若要使用 ADO MD 属性或方法的 ADO 枚举值，你的项目必须引用 ADO 和 ADO MD 库。 例如，你可以使用 ADO **adState**枚举值与 ADO MD[状态](../../../ado/reference/ado-md-api/state-property-ado-md.md)属性。 有关如何建立对库的引用的详细信息，请参阅你的开发工具的文档。  
  
 ADO 对象和方法有关的详细信息，请参阅[ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多维） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多维架构和数据概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)

