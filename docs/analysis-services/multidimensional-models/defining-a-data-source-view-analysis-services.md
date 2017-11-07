---
title: "定义数据源视图 (Analysis Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- names [Analysis Services], data source views
- name matching criteria [Analysis Services]
- Data Source View Wizard
- data source views [Analysis Services], creating
ms.assetid: 0bae4ee4-1742-40e9-bebe-17c788854484
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3aae9714c37d9bd4272add2829d4cdef8f2d9c9d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="defining-a-data-source-view-analysis-services"></a>定义数据源视图 (Analysis Services)
  数据源视图包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维数据库对象（即多维数据集、维度和挖掘结构）使用的架构的逻辑模型。 数据源视图是统一维度模型 (UDM) 和挖掘结构所使用的那些架构元素的元数据定义，以 XML 格式进行存储。 数据源视图：  
  
-   包含表示一个或多个基础数据源中选定对象的元数据，或者包含在您按照自上而下方法生成架构时将用于生成基础关系数据存储的元数据。  
  
-   可以通过一个或多个数据源生成，从而允许您定义将来自多个数据源的数据集成起来的多维和数据挖掘对象。  
  
-   可以包含不在基础数据源中以及独立于基础数据源而存在的关系、主键、对象名、计算列和查询。  
  
-   对于客户端应用程序不可见，也无法由客户端应用程序进行查询。  
  
 DSV 是多维模型的必需组件。 大多数 Analysis Services 开发人员均会在模型设计的初期阶段创建 DSV，以便根据提供基础数据的外部关系数据库生成至少一个 DSV。 但是，您也可以在后面的阶段创建 DSV，以便在创建维度和多维数据集后生成架构和基础数据库结构。 第二种方法有时称为“由上而下设计”，并且通常用于为建模设计原型并进行分析。 在使用此方法时，可使用架构生成向导根据在 Analysis Services 项目或数据库中定义的 OLAP 对象创建基础数据源视图和数据源对象。 不管您如何及何时创建 DSV，每个模型必须具有一个 DSV，然后您才可以处理它。  
  
 本主题包含以下各节：  
  
 [数据源视图构成](#bkmk_dsvdef)  
  
 [使用数据源视图向导创建 DSV](#bkmk_startWiz)  
  
 [指定关系的名称匹配条件](#bkmk_NameMatch)  
  
 [添加辅助数据源](#bkmk_secondaryDS)  
  
##  <a name="bkmk_dsvdef"></a> 数据源视图构成  
 数据源视图包含以下几项：  
  
-   名称和说明。  
  
-   从一个或多个数据源（包括但不超过整个架构）中检索的架构的任何子集的定义，其中包括：  
  
    -   表名。  
  
    -   列名。  
  
    -   数据类型。  
  
    -   为 Null 性。  
  
    -   列长度。  
  
    -   主键。  
  
    -   主键-外键关系。  
  
-   基础数据源中架构的批注，其中包括：  
  
    -   表、视图和列的友好名称。  
  
    -   从一个或多个数据源（在架构中显示为表）返回列的命名查询。  
  
    -   从数据源（在表或视图中显示为列）返回列的命名计算。  
  
    -   逻辑主键（仅当未在基础表中定义主键或者未在视图或命名查询中包含主键时需要）。  
  
    -   表、视图和命名查询之间的逻辑主键-外键关系。  
  
##  <a name="bkmk_startWiz"></a> 使用数据源视图向导创建 DSV  
 若要创建 DSV，请从 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的解决方案资源管理器运行数据源视图向导。  
  
> [!NOTE]  
>  或者，可以使用架构生成向导首先构造维度和多维数据集，然后为模型生成 DSV。 有关详细信息，请参阅[架构生成向导 (Analysis Services)](../../analysis-services/multidimensional-models/schema-generation-wizard-analysis-services.md)。  
  
1.  在解决方案资源管理器中，右键单击 Data Source Views 文件夹，然后单击“新建数据源视图”。  
  
2.  指定向外部关系数据库提供连接信息的新的或现有数据源对象（只能在向导中选择一个数据源）。  
  
3.  在同一页，单击 **“高级”** 以选择特定架构、应用筛选器或排除表关系信息。  
  
     **选择架构**  
  
     对于包含多个架构的超大型数据源，您可以选择要在逗号分隔列表中使用的架构（不包含空格）。  
  
     **检索关系**  
  
     通过在“高级数据源视图选项”对话框中清除 **“检索关系”** 复选框，以允许您在数据源视图设计器中手动创建表之间的关系，您可以故意省略表关系信息。  
  
4.  **筛选可用对象**  
  
     如果可用对象列表包含大量对象，您可以通过应用一个简单的筛选器（指定字符串作为选择条件）减小列表。 例如，如果键入 **dbo** 并单击 **“筛选器”** 按钮，则 **“可用对象”** 列表中只显示以“dbo”开头的那些项。 该筛选器可以为部分字符串（例如，“sal”返回销售额和薪金），但它不能包含多个字符串或运算符。  
  
5.  对于未定义表关系的关系数据源，将显示 **“名称匹配”** 页，以便您可以选择相应的名称匹配方法。 有关详细信息，参阅本主题中的 [指定关系的名称匹配条件](#bkmk_NameMatch) 部分。  
  
##  <a name="bkmk_secondaryDS"></a> 添加辅助数据源  
 定义包含来自多个数据源的表、视图或列的数据源视图时，会将从中将对象添加到数据源视图的第一个数据源指定为主数据源（主数据源在定义之后便不能更改）。 根据来自单个数据源的对象定义数据源视图之后，便可添加来自其他数据源的对象。  
  
 如果 OLAP 处理或数据挖掘查询需要在单个查询中使用来自多个数据源的数据，则主数据源必须支持使用 **OpenRowset**的远程查询。 通常，此数据源将为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源。 例如，如果设计包含绑定到多个数据源列的属性的 OLAP 维度，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将构造 **OpenRowset** 查询以在处理过程中填充此维度。 但是，如果通过单个数据源便可填充 OLAP 对象或解析数据挖掘查询，则不会构造 **OpenRowset** 查询。 在某些情况下，可以定义属性之间的属性关系，从而不再需要 **OpenRowset** 查询。 有关属性关系的详细信息，请参阅 [属性关系](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)、 [在数据源视图中添加或删除表或视图 (Analysis Services)](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md) 和 [定义属性关系](../../analysis-services/multidimensional-models/attribute-relationships-define.md)中的解决方案资源管理器运行数据源视图向导。  
  
 若要从第二个数据源添加表和列，请在解决方案资源管理器中双击 DSV，在数据源视图设计器中打开它，然后使用“添加/删除表”对话框以包含来自在项目中定义的其他数据源中的对象。 有关详细信息，请参阅 [在数据源视图中添加或删除表或视图 (Analysis Services)](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)中的解决方案资源管理器运行数据源视图向导。  
  
##  <a name="bkmk_NameMatch"></a> 指定关系的名称匹配条件  
 创建 DSV 时，将根据数据源中的外键约束创建表之间的关系。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 引擎需要使用这些关系来构造相应的 OLAP 处理查询和数据挖掘查询。 但是，包含多个表的数据源有时并没有外键约束。 如果数据源没有外键约束，则数据源视图向导会提示您定义希望向导如何尝试匹配不同表中的列名。  
  
> [!NOTE]  
>  向导会提示您只有在基础数据源中检测不到外键关系时，才提供名称匹配条件。 如果检测到了外键关系，则使用检测到的关系，您必须手动定义要包括在 DSV 中的任何其他关系（包括逻辑主键）。 有关详细信息，请参阅[在数据源视图中定义逻辑关系 (Analysis Services)](../../analysis-services/multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md) 和[在数据源视图中定义逻辑主键 (Analysis Services)](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md)。  
  
 数据源视图向导将使用您的响应来匹配列名，并创建 DSV 中不同表间的关系。 您可以指定下表中列出的任何一个条件。  
  
|名称匹配条件|Description|  
|----------------------------|-----------------|  
|**与主键同名**|源表中的外键列名与目标表中的主键列名相同。 例如，外键列 `Order.CustomerID` 与主键列 `Customer.CustomerID`相同。|  
|**与目标表同名**|源表中的外键列名与目标表名相同。 例如，外键列 `Order.Customer` 与主键列 `Customer.CustomerID`相同。|  
|**目标表名 + 主键名**|源表中的外键列名为目标表名加上主键列名。 可以使用空格或下划线分隔符。 例如，下列外-主键对完全匹配：<br /><br /> `Order.CustomerID` 和 `Customer.ID`<br /><br /> `Order.Customer ID` 和 `Customer.ID`<br /><br /> `Order.Customer_ID` 和 `Customer.ID`|  
  
 您选择的条件将更改 DSV 的 **NameMatchingCriteria** 属性设置。 此设置确定向导如何添加相关表。 使用数据源视图设计器更改数据源视图时，该规范可确定设计器如何匹配列，从而创建 DSV 中表间的关系。 可以在数据源视图设计器中更改 **NameMatchingCriteria** 属性设置。 有关详细信息，请参阅[在数据源视图中更改属性 (Analysis Services)](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)。  
  
> [!NOTE]  
>  完成数据源视图向导后，可以在数据源视图设计器的架构窗格中添加或删除关系。 有关详细信息，请参阅[在数据源视图中定义逻辑关系 (Analysis Services)](../../analysis-services/multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在数据源视图中添加或删除表或视图 (Analysis Services)](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)   
 [在数据源视图 &#40; 中定义逻辑主键Analysis Services &#41;](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md)   
 [在数据源视图 &#40; 中定义命名的计算Analysis Services &#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [在数据源视图 &#40; 中定义命名的查询Analysis Services &#41;](../../analysis-services/multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)   
 [替换表或数据源视图 &#40; 中的某个命名的查询Analysis Services &#41;](../../analysis-services/multidimensional-models/replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services.md)   
 [使用数据源视图设计器 &#40; 中的关系图Analysis Services &#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [在数据源视图 &#40; 中浏览数据Analysis Services &#41;](../../analysis-services/multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)   
 [删除数据源视图 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/delete-a-data-source-view-analysis-services.md)   
 [刷新数据源视图中的架构 (Analysis Services)](../../analysis-services/multidimensional-models/refresh-the-schema-in-a-data-source-view-analysis-services.md)  
  
  

