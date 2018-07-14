---
title: DataSources 和 DataSets 集合引用（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f951a4aa-da55-4e43-8579-4a5d4480d11f
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 099d9f8ccb24e2675f61c89f277d82984901cd4e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37168148"
---
# <a name="datasources-and-datasets-collection-references-report-builder-and-ssrs"></a>DataSources 和 DataSets 集合引用（报表生成器和 SSRS）
  `DataSources` 集合表示在报表中使用的所有数据源。 同样，`DataSets`集合表示在报表中的所有数据源的所有数据集。 使用 **“报表数据”** 窗格显示报表数据集的层次结构视图，报表数据集按照它们所引用的数据源组织。 如果这些集合中包含引用，则在预览报表时将不会看到值。 这些集合只有在将报表发布到报表服务器之后才可用。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="datasources"></a>DataSources  
 `DataSources` 集合表示在已发布的报表定义中引用的数据源。 您可以选择将此信息包括在报表中，以记录报表数据源。 此集合在 **“预览”** 模式下不可用。 下表对 `DataSources` 集合中的变量进行了说明。  
  
|**变量**|`Type`|**Description**|  
|------------------|--------------|---------------------|  
|`DataSourceReference`|`String`|报表服务器上数据源定义的完整路径。 例如，可以包括用作部分报表历史记录的报表中的所有数据源列表。 下面的示例显示名为 AdventureWorks2012 的数据源的完整路径：<br /><br /> `/DataSources/AdventureWorks2012`的用户。|  
|`Type`|`String`|数据源数据访问接口的类型。 例如， `SQL`。|  
  
## <a name="datasets"></a>DataSets  
 `DataSets` 集合表示在报表定义中引用的数据集。 您可以在文本框中选择包括报表查询，以便希望知道报表中确切数据的用户可以看到原始命令文本。 此集合在 **“预览”** 模式下不可用。 下表介绍的成员`DataSets`集合。  
  
|**成员**|`Type`|**Description**|  
|----------------|--------------|---------------------|  
|`CommandText`|`String`|对于数据库数据源，为用于从数据源中检索数据的查询。 如果查询是一个表达式，则为计算的表达式。|  
|`RewrittenCommandText`|`String`|数据访问接口的扩展 CommandText 值。 它通常用于报表，其中查询参数映射到报表参数。 将命令文本参数引用扩展到为映射的报表参数选中的常量值时，此数据访问接口将设置此属性。|  
  
### <a name="using-query-expressions"></a>使用查询表达式  
 可使用表达式定义包含在数据集中的查询。 您可以使用此功能来设计报表，报表中的查询可以根据用户的输入、其他数据集中的数据或其他变量进行更改。 有关查询的详细信息，请参阅[报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)  
  
  
