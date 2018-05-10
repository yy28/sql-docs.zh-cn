---
title: 编程 AMO OLAP 高级对象 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c07ee6b4289c015b0c42a1bc9981bec29cd49483
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="programming-amo-olap-advanced-objects"></a>AMO OLAP 高级对象的编程
  本主题介绍 OLAP 高级对象的分析管理对象 (AMO) 编程详细信息。 本主题包含以下各节：  
  
-   [操作对象](#Action)  
  
-   [Kpi 对象](#KPI)  
  
-   [透视对象](#Persp)  
  
-   [ProactiveCaching 对象](#PC)  
  
-   [转换对象](#Transl)  
  
##  <a name="Action"></a> 操作对象  
 操作类用于在浏览多维数据集的某些区域时创建活动响应。 Action 对象可通过 AMO 进行定义，但要从浏览数据的客户端应用程序使用这些对象。 操作可为不同类型，因而也就必须根据其类型进行创建。 操作可为：  
  
-   钻取操作，对于在其上执行了该操作的多维数据，该操作将返回表示其所选单元的基础数据的行集。  
  
-   报告操作，对于在其上执行了该操作的多维数据，该操作将从 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 返回一个与其所选部分关联的报表。  
  
-   标准操作，对于在其上执行了该操作的多维数据，该操作将返回与其所选部分关联的操作元素（URL、HTML、DataSet、RowSet 及其他元素）。  
  
 创建 Action 对象需要执行下列步骤：  
  
1.  创建派生的操作对象并填充基本属性。  
  
     以下为基本属性：操作类型、多维数据集的目标类型或部分、多维数据集的目标或特定区域（其中的操作可用）、标题以及标题为 MDX 表达式的位置。  
  
2.  填充操作类型的特定属性。  
  
     三种操作类型的属性各不相同，请参阅随后所示的参数的代码示例。  
  
3.  将操作添加到多维数据集集合，并更新多维数据集。 操作是一个不可更新对象。  
  
 测试操作需要另一个编程应用程序。 可以在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中测试操作。 首先，必须安装[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]示例，请参阅[处理多维模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 下面的示例代码从 Adventure Works Analysis Services 项目示例复制三种不同的操作。 您可以区分这些操作，因为使用以下示例引入的操作以“My”开头。  
  
```  
static public void CreateActions(Cube cube)  
{  
    #region Adding a drillthrough action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Reseller Details"))  
        cube.Actions.Remove("My Drillthrough Action",true);  
  
    //Create a Drillthrough action  
    DrillThroughAction dtaction = new DrillThroughAction("My Reseller Details", "My Drillthrough Action");  
  
    //Define the Action  
    dtaction.Type = ActionType.DrillThrough;  
    dtaction.TargetType = ActionTargetType.Cells;  
    dtaction.Target = "MeasureGroupMeasures(\"Reseller Sales\")";  
    dtaction.Caption = "My Drillthrough...";  
    dtaction.CaptionIsMdx = false;  
  
    #region create drillthrough action specifics  
    //Adding Drillthrough columns  
    //Adding Measure columns to the drillthrough  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Reseller Sales");  
    MeasureBinding mb1 = new MeasureBinding();  
    mb1.MeasureID = mg.Measures.FindByName( "Reseller Sales Amount").ID;  
    dtaction.Columns.Add(mb1);  
  
    MeasureBinding mb2 = new MeasureBinding();  
    mb2.MeasureID = mg.Measures.FindByName("Reseller Order Quantity").ID;  
    dtaction.Columns.Add(mb2);  
  
    MeasureBinding mb3 = new MeasureBinding();  
    mb3.MeasureID = mg.Measures.FindByName("Reseller Unit Price").ID;  
    dtaction.Columns.Add(mb3);  
  
    //Adding Dimension Columns to the drillthrough  
    CubeAttributeBinding cb1 = new CubeAttributeBinding();  
    cb1.CubeID = cube.ID;  
    cb1.CubeDimensionID = cube.Dimensions.FindByName("Reseller").ID;  
    cb1.AttributeID = "Reseller Name";  
    cb1.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb1);  
  
    CubeAttributeBinding cb2 = new CubeAttributeBinding();  
    cb2.CubeID = cube.ID;  
    cb2.CubeDimensionID = cube.Dimensions.FindByName("Product").ID;  
    cb2.AttributeID = "Product Name";  
    cb2.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb2);  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(dtaction);  
    #endregion  
  
    #region Adding a Standard action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My City Map"))  
        cube.Actions.Remove("My Action", true);  
  
    //Create a Drillthrough action  
    StandardAction stdaction = new StandardAction("My City Map", "My Action");  
  
    //Define the Action  
    stdaction.Type = ActionType.Url;  
    stdaction.TargetType = ActionTargetType.AttributeMembers;  
    stdaction.Target = "[Geography].[City]";  
    stdaction.Caption = "\"My View Map for \" + [Geography].[City].CurrentMember.Member_Caption + \"...\"";  
    stdaction.CaptionIsMdx = true;  
  
    #region create standard action specifics  
    stdaction.Expression = "\"http://maps.msn.com/home.aspx?plce1=\" + " +  
        "[Geography].[City].CurrentMember.Name + \",\" + " +  
        "[Geography].[State-Province].CurrentMember.Name + \",\" + " +  
        "[Geography].[Country].CurrentMember.Name + " +  
        "\"&regn1=\" + " +  
        "Case " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Australia] " +  
                "Then \"3\" " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Canada] " +  
                "Or [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[United States] " +  
                "Then \"0\" " +  
                "Else \"1\" " +  
        "End ";  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(stdaction);  
  
    #endregion  
  
    #region Adding a Reporting action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Sales Reason Comparisons"))  
        cube.Actions.Remove("My Report Action", true);  
  
    //Create a Report action  
    ReportAction rsaction = new ReportAction("My Sales Reason Comparisonsp", "My Report Action");  
  
    //Define the Action  
    rsaction.Type = ActionType.Report;  
    rsaction.TargetType = ActionTargetType.AttributeMembers;  
    rsaction.Target = "[Product].[Category]";  
    rsaction.Caption = "\"My Sales Reason Comparisons for \" + [Product].[Category].CurrentMember.Member_Caption + \"...\"";  
    rsaction.CaptionIsMdx = true;  
  
    #region create Report action specifics  
    rsaction.ReportServer = "MyRSSamplesServer";  
    rsaction.Path = "ReportServer?/AdventureWorks Sample Reports/Sales Reason Comparisons";  
    rsaction.ReportParameters.Add("ProductCategory", "UrlEscapeFragment( [Product].[Category].CurrentMember.UniqueName )");  
    rsaction.ReportFormatParameters.Add("rs:Command", "Render");  
    rsaction.ReportFormatParameters.Add("rs:Renderer", "HTML5");  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(rsaction);  
  
    #endregion  
}  
```  
  
##  <a name="KPI"></a> Kpi 对象  
 关键绩效指标 (KPI) 是与多维数据集中的某个度量值组关联并用于评估业务成败的计算集合。 <xref:Microsoft.AnalysisServices.Kpi> 对象可通过 AMO 进行定义，但要从浏览数据的客户端应用程序使用这些对象。  
  
 创建 <xref:Microsoft.AnalysisServices.Kpi> 对象需要执行下列步骤：  
  
1.  创建 <xref:Microsoft.AnalysisServices.Kpi> 对象并填充基本属性。  
  
     以下为基本属性列表：说明、显示文件夹、关联的度量值组和值。 “显示文件夹”属性告知客户端应用程序最终用户应在哪里查找 KPI 才能找到。 “关联的度量值组”属性指示所有 MDX 计算应指向的度量值组。 “值”属性将绩效指标的实际值显示为 MDX 表达式。  
  
2.  定义 KPI 指标：目标、状态和走向。  
  
     指标为计算结果应在 -1 到 1 之间的 MDX 表达式，但定义指标值范围的是浏览应用程序。  
  
3.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中浏览 KPI 时，小于 -1 的值视为 -1，大于 1 的值视为 1。  
  
4.  定义图形图像。  
  
     图形图像为字符串值，在客户端应用程序中用作参考来标识要显示的正确图像集。 图形图像字符串还定义显示函数的行为。 通常，指标范围会分为奇数个状态（从差到好），并且会为每种状态分配一个来自图像集的图像。  
  
     如果您使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 浏览 KPI，则指标范围将根据名称分为三种状态或五种状态。 此外，在有些名称中范围是相反的，-1 指“好”，而 1 指“差”。 在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中，范围内的三种状态如下所示：  
  
    -   差 = -1 到 -0.5  
  
    -   一般 = -0.4999 到 0.4999  
  
    -   好 = 0.50 到 1  
  
     在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中，范围内的五种状态如下所示：  
  
    -   差 = -1 到 -0.75  
  
    -   有风险 = -0.7499 到 -0.25  
  
    -   一般 = -0.2499 到 0.2499  
  
    -   良好 = 0.25 到 0.7499  
  
    -   好 = 0.75 到 1  
  
 下表列出了与图像关联的用法、名称和状态数。  
  
|图像用法|图像名称|状态数|  
|-----------------|----------------|----------------------|  
|状态|形状|3|  
|状态|交通灯|3|  
|状态|路标|3|  
|状态|仪表|3|  
|状态|反向测量|5|  
|状态|温度计|3|  
|状态|柱状|3|  
|状态|面|3|  
|状态|方差箭头|3|  
|走向|标准箭头|3|  
|走向|状态箭头|3|  
|走向|反向状态箭头|5|  
|走向|面|3|  
  
1.  将 KPI 添加到多维数据集集合并更新多维数据集，因为 KPI 是一个不可更新对象。  
  
 测试 KPI 需要另一个编程应用程序。 可以在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中测试 KPI。  
  
 下面的示例代码在“Financial Perpective/Grow Revenue”文件夹中为 Adventure Works Analysis Services 项目示例中包括的 Adventure Works 多维数据集创建 KPI。  
  
```  
static public void CreateKPIs(Cube cube)  
{  
    Kpi kpi = cube.Kpis.Add("My Internet Revenue", "My Internet Revenue");  
    kpi.Description = "(My) Revenue achieved through direct sales via Interner";  
    kpi.DisplayFolder = "\\Financial Perspective\\Grow Revenue";  
    kpi.AssociatedMeasureGroupID = "Internet Sales";  
    kpi.Value = "[Measures].[Internet Sales Amount]";  
    #region Goal  
    kpi.Goal = "Case" +  
               "     When IsEmpty" +  
               "          (" +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          )" +   
               "     Then [Measures].[Internet Sales Amount]" +  
               "     Else 1.10 *" +  
               "          (" +  
               "            [Measures].[Internet Sales Amount]," +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          ) " +  
               " End";  
    #endregion  
    #region Status  
    kpi.Status = "Case" +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .95 " +  
                 "   Then 1 " +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) <  .95 " +  
                 "        And  " +  
                 "        KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .85 " +  
                 "   Then 0 " +  
                 "   Else -1 " +  
                 "End";  
    #endregion  
    #region Trend  
    kpi.Trend = "Case " +  
                "    When VBA!Abs " +  
                "         ( " +  
                "           KpiValue( \"Internet Revenue\" ) -  " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           ) / " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           )   " +  
                "         ) <=.02  " +  
                "    Then 0 " +  
                "    When KpiValue( \"Internet Revenue\" ) -  " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         ) / " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         )  >.02 " +  
                "    Then 1 " +  
                "    Else -1 " +  
                "End";  
    #endregion  
    kpi.TrendGraphic = "Standard Arrow";  
    kpi.StatusGraphic = "Cylinder";  
}.  
```  
  
##  <a name="Persp"></a> 透视对象  
 <xref:Microsoft.AnalysisServices.Perspective> 对象可通过 AMO 进行定义，但要从浏览数据的客户端应用程序使用这些对象。  
  
 创建 <xref:Microsoft.AnalysisServices.Perspective> 对象需要执行下列步骤：  
  
1.  创建 <xref:Microsoft.AnalysisServices.Perspective> 对象并填充基本属性。  
  
     以下为基本属性列表：名称、默认度量值、说明和批注。  
  
2.  添加最终用户应看到的来自父多维数据集的所有对象。  
  
     添加多维数据集维度（属性和层次结构）、度量值组（度量值和度量值组）、操作、KPI 和计算。  
  
3.  将透视添加到多维数据集集合并更新多维数据集，因为透视是一个不可更新对象。  
  
 测试透视需要另一个编程应用程序。 可以在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中测试透视。  
  
 下面的代码示例为提供的多维数据集创建名为“Direct Sales”的透视。  
  
```  
static public void CreatePerspectives(Cube cube)  
{  
    Perspective perspective = cube.Perspectives.Add("Direct Sales", "Direct Sales");  
    CubeDimension dim1 = cube.Dimensions.GetByName("Date");  
    PerspectiveDimension pdim1 = perspective.Dimensions.Add(dim1.DimensionID);  
    pdim1.Attributes.Add("Date");  
    pdim1.Attributes.Add("Calendar Year");  
    pdim1.Attributes.Add("Fiscal Year");  
    pdim1.Attributes.Add("Calendar Quarter");  
    pdim1.Attributes.Add("Fiscal Quarter");  
    pdim1.Attributes.Add("Calendar Month Number");  
    pdim1.Attributes.Add("Fiscal Month Number");  
    pdim1.Hierarchies.Add("Calendar Time");  
    pdim1.Hierarchies.Add("Fiscal Time");  
  
    CubeDimension dim2 = cube.Dimensions.GetByName("Product");  
    PerspectiveDimension pdim2 = perspective.Dimensions.Add(dim2.DimensionID);  
    pdim2.Attributes.Add("Product Name");  
    pdim2.Attributes.Add("Product Line");  
    pdim2.Attributes.Add("Model Name");  
    pdim2.Attributes.Add("List Price");  
    pdim2.Attributes.Add("Size");  
    pdim2.Attributes.Add("Weight");  
    pdim2.Hierarchies.Add("Product Model Categories");  
    pdim2.Hierarchies.Add("Product Categories");  
  
    PerspectiveMeasureGroup pmg = perspective.MeasureGroups.Add("Internet Sales");  
    pmg.Measures.Add("Internet Sales Amount");  
    pmg.Measures.Add("Internet Order Quantity");  
    pmg.Measures.Add("Internet Unit Price");  
  
    pmg = perspective.MeasureGroups.Add("Reseller Sales");  
    pmg.Measures.Add("Reseler Sales Amount");  
    pmg.Measures.Add("Reseller Order Quantity");  
    pmg.Measures.Add("Reseller Unit Price");  
  
    PerspectiveAction pact = perspective.Actions.Add("Drillthrough Action");  
  
    PerspectiveKpi pkpi = perspective.Kpis.Add("Internet Revenue");  
    Cube.Update();  
}  
```  
  
##  <a name="PC"></a> ProactiveCaching 对象  
 <xref:Microsoft.AnalysisServices.ProactiveCaching> 对象可通过 AMO 进行定义。  
  
 创建 <xref:Microsoft.AnalysisServices.ProactiveCaching> 对象需要执行下列步骤：  
  
1.  创建 <xref:Microsoft.AnalysisServices.ProactiveCaching> 对象。  
  
     没有要定义的基本属性。  
  
2.  添加缓存规范。  
  
|规范|Description|  
|-------------------|-----------------|  
|AggregationStorage|用于聚合的存储类型。<br /><br /> 仅适用于分区。 在维度上它必须是**正则。**|  
|SilenceInterval|MOLAP 图像处理启动之前在缓存中存在的最短时间。|  
|滞后时间|最早通知与 MOLAP 图像被破坏时刻之间的时间长度。|  
|SilenceOverrideInterval|在接收初始通知之后，经过多长时间再无条件启动 MOLAP 图像处理。|  
|ForceRebuildInterval|从新 MOLAP 图像被删除开始经过多长时间再无条件（无通知）启动 MOLAP 图像处理。|  
|OnlineMode|MOLAP 图像何时可用。<br /><br /> 可以是**即时**或**OnCacheComplete**。|  
  
1.  将 <xref:Microsoft.AnalysisServices.ProactiveCaching> 对象添加到父集合。 您将需要更新父集合，因为 <xref:Microsoft.AnalysisServices.ProactiveCaching> 是一个不可更新对象。  
  
 下面的代码示例在指定数据库的 Adventure Works 多维数据集中“Internet 销售”度量值组的所有分区中创建 <xref:Microsoft.AnalysisServices.ProactiveCaching> 对象。  
  
```  
static public void SetProactiveCachingSettings(Database db)  
{  
    ProactiveCaching pc;  
    if (db.Cubes.ContainsName("Adventure Works") && db.Cubes.FindByName("Adventure Works").MeasureGroups.ContainsName("Internet Sales"))  
    {  
        ProactiveCachingTablesBinding pctb;  
        TableNotification tn;  
  
        MeasureGroup mg = db.Cubes.FindByName("Adventure Works").MeasureGroups.FindByName("Internet Sales");  
        foreach(Partition part in mg.Partitions)  
        {  
            pc = new ProactiveCaching();  
            pc.AggregationStorage = ProactiveCachingAggregationStorage.MolapOnly;  
            pc.SilenceInterval = TimeSpan.FromSeconds(10);  
            pc.Latency = TimeSpan.FromSeconds(-1);  
            pc.SilenceOverrideInterval = TimeSpan.FromMinutes(10);  
            pc.ForceRebuildInterval = TimeSpan.FromSeconds(-1);  
            pc.Enabled = true;  
            pc.OnlineMode = ProactiveCachingOnlineMode.OnCacheComplete;  
            pctb = new ProactiveCachingTablesBinding();  
            pctb.NotificationTechnique = NotificationTechnique.Server;  
            tn = new TableNotification("[FactInternetSales]", "dbo");  
            pctb.TableNotifications.Add( tn);  
            pc.Source = pctb;  
  
            part.ProactiveCaching = pc;  
            part.Update();  
        }  
    }  
}  
```  
  
##  <a name="Transl"></a> 转换对象  
 Translation 对象可通过 AMO 进行定义，但要从浏览数据的客户端应用程序使用这些对象。 Translation 对象是易于编码的简单对象。 对象标题的翻译由区域设置标识符和翻译后的标题对提供。 对于任何标题，都可以启用多个翻译。 可以为多数 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 对象（例如维度、属性、层次结构、多维数据集、度量值组、度量值以及其他对象）提供翻译。  
  
 下面的代码示例为属性“产品名称”的名称提供了西班牙语翻译。  
  
```  
static public void CreateTranslations(Database db)  
{  
    //Spanish Tranlations for Product Category in Product Dimension  
    Dimension dim = db.Dimensions["Product"];  
    DimensionAttribute atr = dim.Attributes["Product Name"];  
    Translation tran = atr.Translations.Add(3082);  
    tran.Caption = "Nombre Producto";  
  
    dim.Update(UpdateOptions.ExpandFull);  
  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices>   
 [引入 AMO 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO OLAP 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)   
 [逻辑体系结构 & #40;Analysis Services-多维数据 & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象 & #40;Analysis Services-多维数据 & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [处理多维模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [安装适用于 Analysis Services 多维建模教程的示例数据和项目](../../../analysis-services/install-sample-data-and-projects.md)  
  
  
