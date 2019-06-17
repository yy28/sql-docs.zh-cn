---
title: 使用 ADO 与 ADO MD |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2fd684e35c9cebf4a91a0b396e2c8b572e1ecf8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699861"
---
# <a name="using-ado-with-ado-md"></a>使用 ADO 与 ADO MD
ADO 和 ADO MD 相关但独立的对象模型。 ADO 提供的对象用于连接到数据源、 执行命令、 检索表格格式数据和架构元数据以表格格式和查看提供程序错误的信息。 ADO MD 提供用于检索多维数据和查看多维架构元数据的对象。  
  
 当您处理 MDP，您可以选择使用 ADO、 ADO MD 和 / 或与你的应用程序。 通过引用在项目中的这两个库，将具有完全访问权限 MDP 提供的功能。  
  
 它是经常用于使用者能够获取多维数据集的平展的表格视图。 您可以执行此操作使用 ADO[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。 指定的源你[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)作为***源***参数[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**记录集**，而不是作为源ADO MD**单元集**。  
  
 它还可能非常有用，若要查看架构元数据中的表格视图，而不是对象的层次结构。 ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象允许用户打开**记录集**包含架构信息。 ***QueryType***的参数**OpenSchema**方法具有多个[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)与 Mdp 特别相关的值。 其值如下所示：  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 若要使用 ADO MD 属性或方法使用 ADO 枚举值，你的项目必须引用 ADO 和 ADO MD 库。 例如，可以使用 ADO **adState**枚举值与 ADO MD[状态](../../../ado/reference/ado-md-api/state-property-ado-md.md)属性。 有关如何建立对库的引用的详细信息，请参阅你的开发工具的文档。  
  
 ADO 对象和方法有关的详细信息，请参阅[ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)。  
  
## <a name="see-also"></a>请参阅  
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多维） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多维架构和数据的概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 进行编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
