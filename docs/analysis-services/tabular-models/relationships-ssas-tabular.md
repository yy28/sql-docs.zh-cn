---
title: "关系（SSAS 表格） | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21e0144a-3cfd-4bc7-87ff-bb7d1800ed2f
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 27
---
# 关系（SSAS 表格）
  在表格模型中，关系是两个数据表之间的连接。 该关系确立两个表中的数据应该如何相关。 例如，Customers 表和 Orders 表可以彼此相关，以便显示与每个订单关联的客户名称。  
  
 当使用“表导入向导”从相同数据源导入时，选择要导入的表（数据源中）中已存在的关系将在模型中重新创建。 通过使用关系图视图中的模型设计器或使用“管理关系”对话框，可以查看检测到的关系和自动重新创建的关系。 还可以通过使用关系图视图中的模型设计器或使用“创建关系”或“管理关系”对话框，手动创建表之间的新关系。  
  
 在定义了两个表之间的关系（在导入过程中自动创建或手动创建）之后，便能够使用相关列筛选数据以及在相关表中查找值。  
  
> [!TIP]  
>  如果您的模型包含多个关系，则关系图视图可以更好地展现表之间的关系和创建新关系。  
  
 本主题的内容：  
  
-   [优势](#what)  
  
-   [关系的要求](#requirements)  
  
-   [关系的推理](#detection)  
  
-   [导入数据时检测关系](#bkmk_detection)  
  
-   [手动创建关系](#bkmk_manually_create)  
  
-   [重复的值和其他错误](#bkmk_dupl_errors)  
  
-   [相关任务](#bkmk_related_tasks)  
  
##  <a name="what"></a> 优势  
 关系是两个数据表之间的连接，它基于每个表中的一列或多列。 要理解关系为何有用，可以想像一下在业务中跟踪客户订单数据。 可以在具有以下结构的一个表中跟踪所有数据：  
  
|CustomerID|名称|EMail|DiscountRate|OrderID|OrderDate|Product|Quantity|  
|----------------|----------|-----------|------------------|-------------|---------------|-------------|--------------|  
|1|Ashton|chris.ashton@contoso.com|.05|256|2010-01-07|Compact Digital|11|  
|1|Ashton|chris.ashton@contoso.com|.05|255|2010-01-03|SLR Camera|15|  
|2|Jaworski|michal.jaworski@contoso.com|.10|254|2010-01-03|Budget Movie-Maker|27|  
  
 这种方法可以用，但会存储大量冗余数据，如每个订单的客户电子邮件地址。 存储成本低廉，但如果电子邮件地址发生更改，就必须确保更新该客户的每一行数据。 针对这一问题，一种解决方法是将数据拆分到多个表中，然后在这些表之间定义关系。 这就是关系数据库  （如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）中使用的方法。 例如，导入模型的某个数据库可以使用三个相关表来表示订单数据：  
  
### Customers  
  
|[CustomerID]|名称|EMail|  
|--------------------|----------|-----------|  
|1|Ashton|chris.ashton@contoso.com|  
|2|Jaworski|michal.jaworski@contoso.com|  
  
### CustomerDiscounts  
  
|[CustomerID]|DiscountRate|  
|--------------------|------------------|  
|1|.05|  
|2|.10|  
  
### Orders  
  
|[CustomerID]|OrderID|OrderDate|Product|Quantity|  
|--------------------|-------------|---------------|-------------|--------------|  
|1|256|2010-01-07|Compact Digital|11|  
|1|255|2010-01-03|SLR Camera|15|  
|2|254|2010-01-03|Budget Movie-Maker|27|  
  
 如果从同一数据库导入这些表，则“表导入向导”可以根据 [方括号] 中的列来检测这些表之间的关系，并可以在模型设计器中再现这些关系。 有关详细信息，请参阅本主题中的 [关系的自动检测和推理](#detection) 。 如果从多个源导入表，则可以手动创建关系，如[创建两个表之间的关系（SSAS 表格）](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)所述。  
  
### 列和键  
 关系基于每个表中包含相同数据的列。 例如，Customers 和 Orders 表可以彼此相关，因为它们都包含存储客户 ID 的列。 在本示例中，列名称相同，但这不是必需的。 只要 Orders 表的所有行都包含也存储在 Customers 表中的 ID，一列可以是 CustomerID，另一列可以是 CustomerNumber。  
  
 在关系数据库中，有几种类型的键 ，键通常是具有指定属性的列。 在关系数据库中，可以使用以下四种类型的键：  
  
-   *主键*：唯一标识表中的一行，如 Customers 表中的 CustomerID。  
  
-   *备用键*（或*候选键*）：主键之外的唯一列。 例如，Employees 表可能存储雇员 ID 和社会保障号，这两者都是唯一的。  
  
-   *外键*：引用另一表中唯一列的列，如 Orders 表中的 CustomerID（可引用 Customers 表中的 CustomerID）。  
  
-   组合键：由多列组成的键。 表格模型中不支持组合键。 有关详细信息，请参阅本主题中的“组合键和查找列”。  
  
 在表格模型中，主键或备用键称为“相关查找列” 或“查找列” 。 如果表既有主键又有备用键，则主键和备用键都可作为查找列。 外键称为“源列”  或简单地称为“列” 。 在我们的示例中，将在 Orders 表的 CustomerID（列）和 Customers 表的 CustomerID（查找列）之间定义关系。 如果从关系数据库导入数据，默认情况下，模型设计器会从一个表中选择外键，从另一个表中选择相应的主键。 但是，您可以将具有唯一值的任意列用作查找列。  
  
### 关系类型  
 Customers 与 Orders 之间的关系是“一对多关系”。 每个客户都可以有多个订单，但一个订单不能有多个客户。 其他关系类型还有“一对一”和“多对多”。 为每个客户定义一个折扣率的 CustomerDiscounts 表与 Customers 表具有一对一关系。 Products 和 Customers 之间的直接关系就是多对多关系的一个示例，在这种关系中，一个客户可以购买多种产品，同一种产品可由很多客户购买。 在用户界面中，模型设计器不支持多对多关系。 有关详细信息，请参阅本主题中的[多对多关系](#bkmk_many_to_many)。  
  
 下表显示了三个表之间的关系：  
  
|关系|类型|查找列|列|  
|------------------|----------|-------------------|------------|  
|Customers-CustomerDiscounts|一对一|Customers.CustomerID|CustomerDiscounts.CustomerID|  
|Customers-Orders|一对多|Customers.CustomerID|Orders.CustomerID|  
  
### 关系和性能  
 在创建任何关系之后，对于任何公式，如果它们使用新创建的关系中所涉及的各表中的列，模型设计器通常必须对其进行重新计算。 处理可能需要一些时间，这取决于数据量和关系的复杂度。  
  
##  <a name="requirements"></a> 关系的要求  
 创建关系时，模型设计器必须遵守几项要求：  
  
### 表之间的单个活动关系  
 多个关系会导致表之间存在不明确的依赖关系。 若要创建准确的计算，需要从一个表到下一个表的单一路径。 因此，每对表之间只能存在一个活动关系。 例如，在 AdventureWorks DW 2012 中，表 DimDate 包含一个列 DateKey，该列与表 FactInternetSales 中的以下三个不同列相关：OrderDate、DueDate 和 ShipDate。 如果您试图导入这些表，则会成功创建第一个关系，但是在创建涉及相同列的后续关系时会接收到下面的错误：  
  
 \* 关系: 表[列 1]-> 表[列 2]   - 状态: 错误   - 原因: 在表 \<表 1> 和 \<表 2> 之间无法创建关系。 在两个表之间只能存在一个直接或间接关系。  
  
 如果您有两个表并且这两个表之间存在多个关系，则需要导入包含查找列的表的多个副本，并在每对表之间创建一个关系。  
  
 表之间可以有许多非活动关系。 表之间要使用的路径在查询时由报表客户端指定。  
  
### 每个源列具有一个关系  
 源列无法具有多个关系。 如果您已在一个关系中将某列用作源列，但希望使用该列连接到其他表中的另一个相关的查找列，则可以创建该列的副本并使用该列创建新的关系。  
  
 可使用计算列中的 DAX 公式轻松创建具有完全相同值的列的副本。 有关详细信息，请参阅[创建计算列（SSAS 表格）](../../analysis-services/tabular-models/create-a-calculated-column-ssas-tabular.md)。  
  
### 每个表的唯一标识符  
 每个表都必须具有一个单独的列，用于唯一标识该表中的每一行。 该列通常称为主键。  
  
### 唯一查找列  
 查找列中的数据值必须是唯一的。 也就是说，该列不能包含重复值。 在表格模型中，Null 和空字符串等效于空白，而空白是一种独特的数据值。 这意味着查找列中不能包含多个 Null 值。  
  
### 兼容的数据类型  
 源列和查找列中的数据类型必须兼容。 有关数据类型的详细信息，请参阅[支持的数据类型（SSAS 表格）](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)。  
  
### 组合键和查找列  
 不能在表格模型中使用组合键；必须始终有一列来唯一标识表中的每一行。 如果您试图导入的表中包含基于组合键的现有关系，表导入向导会忽略该关系，因为在表格模型中无法创建该关系。  
  
 如果要在模型设计器中创建两个表之间的关系，并且存在多个定义主键和外键的列，必须先组合这些值创建一个键列，然后才能创建关系。 您可以在导入数据之前执行此操作，也可以在模型设计器中通过创建计算列来执行此操作。  
  
###  <a name="bkmk_many_to_many"></a> 多对多关系  
 表格模型不支持多对多关系，不能在模型设计器中添加“联接表”。 但可以使用 DAX 函数为多对多关系建模。  
  
 你还可以尝试设置双向交叉筛选器以查看它是否实现同一目的。 有时，可以通过跨多个表关系保持筛选器上下文的交叉筛选器，来满足多对多关系的要求。 有关详细信息，请参阅 [SQL Server 2016 Analysis Services 中适用于表格模型的双向交叉筛选器](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)。  
  
### 自联接和循环  
 表格模型表中不允许使用自联接。 自联接是一个表与其自身之间的递归关系。 自联接通常用于定义父子层次结构。 例如，可以将 Employees 表联接到其自身，从而生成显示业务管理链的层次结构。  
  
 模型设计器不允许在模型中的关系之间创建循环。 换言之，禁止使用下面这组关系。  
  
 表 1、列 a 到表 2、列 f  
  
 表 2、列 f 到表 3、列 n  
  
 表 3、列 n 到表 1、列 a  
  
 如果您试图创建的关系会导致创建循环，则会生成错误。  
  
##  <a name="detection"></a> 关系的推理  
 在某些情况下，表之间的关系会自动链接。 例如，如果在以下前两组表之间创建关系，则会推断出其他两个表之间存在一个关系，进而自动建立一个关系。  
  
 Products 和 Category -- 手动创建  
  
 Category 和 SubCategory -- 手动创建  
  
 Products 和 SubCategory -- 推断出关系  
  
 为使关系自动链接，关系方向必须相同，如上所示。 例如，如果初始关系是在 Sales 和 Products 以及 Sales 和 Customers 之间，则不会推断出关系。 这是因为 Products 和 Customers 之间的关系是多对多关系。  
  
##  <a name="bkmk_detection"></a> 导入数据时检测关系  
 从关系数据源表中导入时，表导入向导将基于源架构数据检测这些源表中的现有关系。 如果导入相关的表，则将在模型中复制这些关系。  
  
##  <a name="bkmk_manually_create"></a> 手动创建关系  
 尽管单个关系数据源中的表之间的大多数关系将会被自动检测到并且在表格模型中创建，但还有许多必须手动创建模型表之间的关系的情况。  
  
 如果您的模型中包含来自多个数据源的数据，则可能需要手动关系。 例如，您可以从关系数据源导入 Customers、CustomerDiscounts 和 Orders 表。 在源中的这些表之间存在的关系将在模型中自动创建。 然后，您可以添加来自不同源的其他表，例如，从 Microsoft Excel 工作簿中的 Geography 表导入区域数据。 然后，您可以手动在 Customers 表中的某一列和 Geography 表中的某一列之间创建关系。  
  
 若要手动在表格模型中创建关系，您可以使用关系图视图中的模型设计器或使用“管理关系”对话框。 关系图视图以图形格式显示表以及表之间的关系。 您可以单击一个表中的某一列，将该列拖放到其他表中以便轻松地在两个表之间以正确顺序创建关系。 “管理关系”对话框会以简单的表格式显示表之间的关系。 了解如何手动创建关系，请参阅[创建两个表之间的关系（SSAS 表格）](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)。  
  
##  <a name="bkmk_dupl_errors"></a> 重复的值和其他错误  
 如果选择了在关系中不能使用的列，该列旁边将出现一个红色的 X。 您可以将光标暂停在错误图标之上，以查看提供有关该问题的详细信息的消息。 导致无法在所选列之间创建关系的问题包括：  
  
|问题或消息|解决方法|  
|------------------------|----------------|  
|无法创建关系，因为这两个选定的列包含重复值。|若要创建有效的关系，您所选的一对列中应至少有一列必须包含唯一值。<br /><br /> 您可以编辑列来删除重复值，也可以反转列的顺序，以便将包含唯一值的列用作 **“相关查找列”**。|  
|该列包含 Null 值或空值。|对于 Null 值，无法将数据列相互联接。 对于每一行，关系中所用的两列都必须具有值。|  
  
##  <a name="bkmk_related_tasks"></a> 相关任务  
  
|主题|Description|  
|-----------|-----------------|  
|[创建两个表之间的关系（SSAS 表格）](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)|介绍如何手动创建两个表之间的关系。|  
|[删除关系（SSAS 表格）](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)|描述如何删除关系和删除关系带来的后果。|  
|[SQL Server 2016 Analysis Services 中适用于表格模型的双向交叉筛选器](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)|描述相关表的双向交叉筛选。 如果两个表是相关的，且定义了双向交叉筛选器，则当跨第二个表关系查询时，可以使用第一个表关系的筛选上下文。|  
  
## 另请参阅  
 [表和列（SSAS 表格）](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [导入数据（SSAS 表格）](../Topic/Import%20Data%20\(SSAS%20Tabular\).md)  
  
  