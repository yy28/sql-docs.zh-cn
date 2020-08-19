---
description: 使用 ADO 与 ADO MD
title: 将 ADO 用于 ADO MD |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6314ae9a0682e1c10b1ecd45c8f8d5217e7d6426
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452399"
---
# <a name="using-ado-with-ado-md"></a>使用 ADO 与 ADO MD
ADO 和 ADO MD 与不同的对象模型相关。 ADO 提供用于连接到数据源、执行命令、以表格格式检索表格数据和架构元数据以及查看提供程序错误信息的对象。 ADO MD 提供用于检索多维数据和查看多维架构元数据的对象。  
  
 当使用 MDP 时，可以选择将 ADO 和/或 ADO MD 用于应用程序。 通过在你的项目中引用这两个库，你将对 MDP 提供的功能具有完全访问权限。  
  
 通常，使用者可以获取多维数据集的平展表格视图。 可以通过使用 ADO [记录集](../../../ado/reference/ado-api/recordset-object-ado.md) 对象来执行此操作。 指定[单元](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)集的源作为**记录集**的[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法的***源***参数，而不是作为 ADO MD**单元集**的源。  
  
 在表格视图中查看架构元数据（而不是对象的层次结构）可能也很有用。 使用[Connection](../../../ado/reference/ado-api/connection-object-ado.md)对象上的 ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md)方法，用户可以打开包含架构信息的**记录集**。 **OpenSchema**方法的***QueryType***参数具有几个特定于 MDPs 的[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)值。 其值如下所示：  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 若要在 ADO MD 属性或方法中使用 ADO 枚举值，你的项目必须同时引用 ADO 和 ADO MD 库。 例如，可以将 ADO **adState** 枚举值用于 ADO MD [状态](../../../ado/reference/ado-md-api/state-property-ado-md.md) 属性。 有关如何建立对库的引用的详细信息，请参阅开发工具的文档。  
  
 有关 ADO 对象和方法的详细信息，请参阅 [ADO API 参考](../../../ado/reference/ado-api/ado-api-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (多维)  (ADO MD) ](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多维架构和数据的概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [用 ADO MD 进行编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
