---
title: 模糊查找转换编辑器（"引用表" 选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.referencetable.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: 451f4e7d-1c8e-4784-b540-df0806509bf1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eb86e4a6382095bb8bb0edc744fe6d16650581fd
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425204"
---
# <a name="fuzzy-lookup-transformation-editor-reference-table-tab"></a>模糊查找转换编辑器（“引用表”选项卡）
  使用 **“模糊查找转换编辑器”** 对话框的 **“引用表”** 选项卡可以指定用于查找的源表和索引。 引用数据源必须是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中的表。  
  
> [!NOTE]  
>  模糊查找转换将创建引用表的工作副本。 下面描述的索引是通过使用特殊的表对此工作表创建的，它们不是普通的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 索引。 除非选择了 **“维护存储的索引”**，否则转换不会修改现有的源表。 在这种情况下，转换将对引用表创建一个触发器，此触发器将基于对引用表所做的更改来更新工作表和查找索引表。  
  
> [!NOTE]  
>  `Exhaustive`模糊查找转换的和 `MaxMemoryUsage` 属性在 "**模糊查找转换编辑器**" 中不可用，但可以使用 "**高级编辑器**" 进行设置。 此外，只能 `MaxOutputMatchesPerInput` 在**高级编辑器**中指定大于100的值。 有关这些属性的详细信息，请参阅 [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md)的“模糊查找转换”部分。  
  
 若要了解有关模糊查找转换的详细信息，请参阅 [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md)。  
  
## <a name="options"></a>选项  
 **OLE DB 连接管理器**  
 从列表中选择现有的 OLE DB 连接管理器，或通过单击“新建”**** 创建一个新连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”**** 对话框创建新的连接。  
  
 **生成新索引**  
 指定转换应创建新的索引以用于查找。  
  
 **引用表的名称**  
 选择要用作引用（查找）表的现有表。  
  
 **存储新索引**  
 如果希望保存新的查找索引，请选择此选项。  
  
 **新索引名称**  
 如果已选择保存新的查找索引，请为其键入描述性名称。  
  
 **“维护存储的索引”**  
 如果已选择保存新的查找索引，请指定是否还希望 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 维护该索引。  
  
> [!NOTE]  
>  如果在 **“模糊查找转换编辑器”** 的 **“引用表”** 选项卡中选择 **“维护存储的索引”**，则转换将使用托管存储过程维护索引。 这些托管存储过程使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的公共语言运行时 (CLR) 集成功能。 默认情况下，不启用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 CLR 集成。 若要使用 **“维护存储的索引”** 功能，必须启用 CLR 集成。 有关详细信息，请参阅 [Enabling CLR Integration](../relational-databases/clr-integration/clr-integration-enabling.md)。  
>   
>  由于 **“维护存储的索引”** 选项需要 CLR 集成，所以只有在选择已启用 CLR 集成的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上的引用表时，此功能才能发挥作用。  
  
 **使用现有索引**  
 指定转换应使用现有索引来执行查找。  
  
 **现有索引的名称**  
 从列表中选择以前创建的查找索引。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [模糊查找转换编辑器 &#40;列 "选项卡&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [模糊查找转换编辑器（“高级”选项卡）](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
