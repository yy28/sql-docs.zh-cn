---
title: 双向交叉筛选器在表格模型中 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb5fe85608ebe584966c35f61eb749a4a128da5f
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="bi-directional-cross-filters-in-tabular-models"></a>在表格模型中的双向交叉筛选器
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  SQL Server 2016 中新增一项内置功能，可让你在表格模型中启用“双向交叉筛选器”，从而无需手动制定 DAX 解决方法来传播跨表上下文的筛选器上下文。  
  
 让我们分解这一概念的各个组成部分：“交叉筛选”是指能够基于相关表中的值对表设置筛选器上下文，“双向”是指将筛选器上下文传输到位于表关系另一端的另一个相关表。 顾名思义，你可以朝关系的两个方向而不只是一个方向切片。  在内部，双向筛选可以扩展筛选器上下文以查询数据的超集。  
  
 ![SSAS-BIDI-1-Filteroption](../../analysis-services/tabular-models/media/ssas-bidi-1-filteroption.PNG "SSAS-BIDI-1-Filteroption")  
  
 有两种类型的交叉筛选器： 单向和双向筛选。 单向筛选是在该关系中的事实表与维度表之间进行传统的多对一筛选。 双向筛选是一种交叉筛选，可将一个关系的筛选器上下文用作另一个表关系的筛选器上下文，其中，一个表由两个关系共用。  
  
 在指定 **DimDate** 和 **DimProduct** 的情况下，如果外键关系为 **FactOnlineSales**，则双向交叉筛选器等效于同时使用 **FactOnlineSales-to-DimDate** 和 **FactOnlineSales-to-DimProduct** 。  
  
 使用双向交叉筛选器可以轻松解决表格和 Power Pivot 开发人员过去经常遇到的多对多查询设计难题。 如果你对表格或 Power Pivot 模型中的多对多关系用过 DAX 解决方法，可以尝试应用双向筛选器，以确定是否能够产生预期的结果。  
  
 在创建双向交叉筛选时，请记住以下几点：  
  
-   在启用双向筛选器之前认真思考。  
  
     如果在每个位置都启用双向筛选器，则你的数据可能会过度筛选，这不是你想要的结果。  如果创建多个潜在的查询路径，可能会无意中造成歧义。 若要避免这两种问题，可计划使用单向和双向筛选器的组合。  
  
-   执行增量测试，以验证每次更改筛选器对模型的影响。 [在 Excel 中分析](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md) 非常适用于增量测试。 最佳实践是定期使用其他报告客户端进行测试以跟踪影响，以免将来不知所措。  
  
> [!NOTE]  
>  从 CTP 3.2 开始，SSDT 包括一个用于确定是否应自动尝试双向交叉筛选器的默认设置。 如果你按默认启用双向筛选器，则仅当模型通过表关系链明确指定了一个查询路径时，SSDT 才启用双向筛选。  
  
## <a name="set-the-default"></a>设置默认选项  
 单向筛选器是默认选项。 你可以更改在设计器中创建的所有新项目的默认选项；如果该项目已存在，则可以在模型本身上更改默认选项。  
  
 从项目级别来看，当你创建项目时，将会评估设置，因此，如果你将默认选项更改为双向，将在创建下一个项目时看到选定项的效果。  
  
1.  在 SSDT 中，选择“工具” > “选项” > “Analysis Services 表格设计器” > “新项目设置”。  
  
2.  将“默认筛选器方向”设置为“单向”或“双向”。  
  
 或者，你可以在模型上更改默认方向。  
  
1.  在解决方案资源管理器中，选择“Model.bim” > “属性”。  
  
2.  将“默认筛选器方向”设置为“单向”或“双向”。  
  
## <a name="walkthrough-an-example"></a>演练示例  
 最好是通过一个示例来理解双向交叉筛选的值。 假设 [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279)中有以下数据集，该数据集反映按默认创建的基数和交叉筛选器。  
  
 ![SSAS 双向 2 模型](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "SSAS 双向 2 模型")  
  
> [!NOTE]  
>  默认情况下，在数据导入期间，将在派生自事实数据表与相关维度表之间的外键和主键关系的多对一配置中为你创建表关系。  
  
 请注意，筛选方向是从维度表到事实数据表 - 促销、产品、日期、客户和客户地理位置都是有效的筛选器，可成功产生度量值的某种聚合，实际值根据使用的维度而有所不同。  
  
 ![ssas 双向 3 defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "ssas 双向 3 defaultrelationships")  
  
 对于这种简单的星型架构，在筛选从维度表中行与列到位于中心 **FactOnlineSales** 表的“销售额总计”度量值提供的聚合数据的数据流时，Excel 中的测试可以完美地确认数据切片。   
  
 ![ssas-bidi-4-excelSumSales](../../analysis-services/tabular-models/media/ssas-bidi-4-excelsumsales.PNG "ssas-bidi-4-excelSumSales")  
  
 只要度量值是从事实数据表中提取的并且筛选器上下文在事实数据表上终止，就能为此模型正确筛选聚合。 但是，如果你想要在其他位置创建度量值（例如，在产品或客户表中创建非重复计数，或者在促销表中创建平均折扣），并且现有的筛选器上下文将扩展到该度量值，那么会发生什么情况呢？  
  
 让我们尝试将 **DimProducts** 中的非重复计数添加到数据透视表以查看结果。 请注意“产品计数”的重复值。  从表面看，似乎缺少一种表关系，但在我们的模型中可以看到，所有关系都已完全定义并处于活动状态。 在这种情况下，之所以出现重复值，是因为没有针对产品表中的行设置日期筛选器。  
  
 ![ssas-bidi-5-prodcount-nofilter](../../analysis-services/tabular-models/media/ssas-bidi-5-prodcount-nofilter.png "ssas-bidi-5-prodcount-nofilter")  
  
 在 **FactOnlineSales** 和 **DimProduct**之间添加双向交叉筛选器后，可以按制造商和日期正确筛选产品表中的行。  
  
 ![ssas-bidi-6-prodcount-withfilter](../../analysis-services/tabular-models/media/ssas-bidi-6-prodcount-withfilter.png "ssas-bidi-6-prodcount-withfilter")  
  
## <a name="learn-step-by-step"></a>了解分步  
 可以通过逐步学习本演练来尝试使用双向交叉筛选器。 若要继续，你需要：  
  
-   安装表格模式的 SQL Server 2016 Analysis Services 实例及其最新 CTP 版本  
  
-   随最新 CTP 版本一起发行的[SQL Server Data Tools for Visual Studio 2015 (SSDT)](http://go.microsoft.com/fwlink/p/?LinkID=627574)。  
  
-   [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279)  
  
-   对此数据的读取权限。  
  
-   Excel（以便使用“在 Excel 中分析”）  
  
### <a name="create-a-project"></a>创建项目  
  
1.  启动 SQL Server Data Tools for Visual Studio 2015。  
  
2.  单击“文件” > “新建” > “项目” > “Analysis Services 表格模型”。  
  
3.  在表格模型设计器中，将工作区数据库设置为表格服务器模式的 SQL Server 2016 Preview Analysis Services 实例。  
  
4.  验证模型兼容性级别设置为**SQL Server 2016 RTM (1200)** 或更高版本。  
  
     单击 **“确定”** 以创建项目。  
  
### <a name="add-data"></a>添加数据  
  
1.  单击“模型” > “从数据源导入” > “Microsoft SQL Server”。  
  
2.  指定服务器、数据库和身份验证方法。  
  
3.  选择 ContosoRetailDW 数据库。  
  
4.  单击“下一步” 。  
  
5.  在选择表时，请按住 Ctrl 的同时选择以下表：  
  
    -   FactOnlineSales  
  
    -   DimCustomer  
  
    -   DimDate  
  
    -   DimGeography  
  
    -   DimPromotion  
  
     如果你希望表的名称在模型中更容易识别，你现在可以编辑名称。  
  
     ![ssas-bidi-7-ImportData](../../analysis-services/tabular-models/media/ssas-bidi-7-importdata.PNG "ssas-bidi-7-ImportData")  
  
6.  导入数据。  
  
 如果出现错误，请确认用于连接到数据库的帐户的 SQL Server 登录名是否对 Contoso 数据仓库拥有读取权限。 在建立远程连接时，你可能还要检查 SQL Server 防火墙中的端口配置。  
  
### <a name="review-default-table-relationships"></a>查看默认表关系  
 切换到关系图视图：“模型” > “模型视图” > “关系图视图”。 将直观指示基数和活动关系。 任意两个相关表之间的所有关系都是一对多的关系。  
  
 ![SSAS 双向 2 模型](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "SSAS 双向 2 模型")  
  
 或者，单击“表” > “管理关系”查看表布局中的相同信息。  
  
 ![ssas 双向 3 defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "ssas 双向 3 defaultrelationships")  
  
### <a name="create-measures"></a>创建度量值  
 需要使用一个聚合来根据维度数据的不同 facet 来合计销售额。 在 **DimProduct** 中，可以创建一个统计产品的度量值，然后使用该度量值来分析产品销售情况，以显示在给定年份、在给定区域或针对哪种客户类型销售了多少产品。  
  
1.  单击“模型” > “模型视图” > “关系图视图”。  
  
2.  单击“FactOnlineSales”。   
  
3.  选择“SalesAmount”列。   
  
4.  单击“列” > “自动求和” > “求和”以创建销售度量值。  
  
5.  单击“DimProduct”。   
  
6.  选择“ProductKeycolumn”。   
  
7.  单击“列” > “自动求和” > “非重复计数”，以创建独特产品的度量值。  
  
### <a name="analyze-in-excel"></a>在 Excel 中分析  
  
1.  单击“模型” > “在 Excel 中分析”，以便在数据透视表中聚合所有数据。  
  
2.  选择你刚刚从字段列表创建的两个度量值。  
  
3.  选择“产品” > “制造商”。  
  
4.  选择“日期” > “日历年”。  
  
 可以看到，销售已根据预期按年份和制造商划分。 这是因为 **FactOnlineSales**、 **DimProduct**与 **DimDate** 之间的默认筛选器上下文对关系的“多”侧的度量值起了作用。  
  
 同时，你可以看到，产品计数未选择与销售一样的筛选器上下文。 尽管产品计数已按制造商正确筛选（制造商和产品计数在同一个表中），但日期筛选器未传播到产品计数。  
  
### <a name="change-the-cross-filter"></a>更改交叉筛选器  
  
1.  返回到模型，选择“表” > “管理关系”。  
  
2.  编辑 **FactOnlineSales** 与 **DimProduct**之间的关系。  
  
     将筛选方向更改为指向这两个表。  
  
3.  保存设置。  
  
4.  在工作簿中，单击“刷新”以重新读取模型。  
  
 现在，你应会看到，产品和销售已按相同的筛选器上下文进行筛选，不仅包括 **DimProducts** 中的制造商，而且包括 **DimDate**中的日历年。  
  
## <a name="next-steps"></a>后续步骤  
 了解何时与如何使用双向交叉筛选器来试错，以及双向交叉筛选器在你方案中的工作方式。 有时，你会发现内置行为并不足够，需要撤销 DAX 计算才能完成作业。 **另请参阅** 部分中提供了有关此主题的其他资源的多个链接。  
  
 实际上，交叉筛选可以实现通常只能通过多对多构造实现的数据探索形式。 尽管如此，你必须认识到双向交叉筛选并不是一种多对多构造。  此版本中的表格模型设计器仍不支持实际的多对多表配置。  
  
## <a name="see-also"></a>另请参阅  
 [在 Power BI Desktop 中创建和管理关系](https://support.powerbi.com/knowledgebase/articles/464155-create-and-manage-relationships-in-power-bi-desktop)   
 [如何处理在 Power Pivot 和表格模型中的简单多到 manay 关系一个实际示例](http://social.technet.microsoft.com/wiki/contents/articles/22202.a-practical-example-of-how-to-handle-simple-many-to-many-relationships-in-power-pivotssas-tabular-models.aspx)   
 [利用 DAX 的解析多对多关系交叉表筛选](http://blog.gbrueckl.at/2012/05/resolving-many-to-many-relationships-leveraging-dax-cross-table-filtering/)   
 [多对多 revolution （SQLBI 博客）](http://www.sqlbi.com/articles/many2many/)  
  
  
