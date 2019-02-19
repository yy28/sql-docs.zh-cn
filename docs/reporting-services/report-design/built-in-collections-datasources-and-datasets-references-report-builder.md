---
title: DataSources 和 DataSets 集合引用（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: f951a4aa-da55-4e43-8579-4a5d4480d11f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1290f2813d11c53e91dc233c6ffa1c065a824f0f
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295566"
---
# <a name="built-in-collections---datasources-and-datasets-references-report-builder"></a>内置集合 - 数据源和数据集引用（报表生成器）
  **DataSources** 集合表示在报表中使用的所有数据源。 同样， **DataSets** 集合表示报表中所有数据源的所有数据集。 使用 **“报表数据”** 窗格显示报表数据集的层次结构视图，报表数据集按照它们所引用的数据源组织。 如果这些集合中包含引用，则在预览报表时将不会看到值。 这些集合只有在将报表发布到报表服务器之后才可用。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="datasources"></a>DataSources  
 **DataSources** 集合表示在已发布的报表定义中引用的数据源。 您可以选择将此信息包括在报表中，以记录报表数据源。 此集合在 **“预览”** 模式下不可用。 下表对 **DataSources** 集合中的变量进行了说明。  
  
|**变量**|**类型**|**Description**|  
|------------------|--------------|---------------------|  
|**DataSourceReference**|**String**|报表服务器上数据源定义的完整路径。 例如，可以包括用作部分报表历史记录的报表中的所有数据源列表。 下面的示例显示名为 AdventureWorks2012 的数据源的完整路径：<br /><br /> `/DataSources/AdventureWorks2012`。|  
|**类型**|**String**|数据源数据访问接口的类型。 例如， `SQL`。|  
  
## <a name="datasets"></a>DataSets  
 **DataSets** 集合表示在报表定义中引用的数据集。 您可以在文本框中选择包括报表查询，以便希望知道报表中确切数据的用户可以看到原始命令文本。 此集合在 **“预览”** 模式下不可用。 下表对 **DataSets** 集合的成员进行了说明。  
  
|**成员**|**类型**|**Description**|  
|----------------|--------------|---------------------|  
|**CommandText**|**String**|对于数据库数据源，为用于从数据源中检索数据的查询。 如果查询是一个表达式，则为计算的表达式。|  
|**RewrittenCommandText**|**String**|数据访问接口的扩展 CommandText 值。 它通常用于报表，其中查询参数映射到报表参数。 将命令文本参数引用扩展到为映射的报表参数选中的常量值时，此数据访问接口将设置此属性。|  
  
### <a name="using-query-expressions"></a>使用查询表达式  
 可使用表达式定义包含在数据集中的查询。 您可以使用此功能来设计报表，报表中的查询可以根据用户的输入、其他数据集中的数据或其他变量进行更改。 有关查询的详细信息，请参阅[报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
