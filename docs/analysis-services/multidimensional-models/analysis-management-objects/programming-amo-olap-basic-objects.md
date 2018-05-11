---
title: 编程 AMO OLAP Basic Objects |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b75256253cc9b40c73705fbbb6d74fd92374bd66
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="programming-amo-olap-basic-objects"></a>AMO OLAP 基本对象的编程
  创建复杂 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 对象是一个简单直接的过程，但需要注意细节。 本主题介绍 OLAP 基本对象的编程详细信息。 本主题包含以下各节：  
  
-   [维度对象](#Dim)  
  
-   [多维数据集对象](#Cub)  
  
-   [度量值组对象](#MG)  
  
-   [分区对象](#Part)  
  
-   [聚合对象](#AD)  
  
##  <a name="Dim"></a> 维度对象  
 若要管理或处理维度，需要对 <xref:Microsoft.AnalysisServices.Dimension> 对象进行编程。  
  
### <a name="creating-dropping-and-finding-a-dimension"></a>创建、删除和查找维度  
 创建 <xref:Microsoft.AnalysisServices.Dimension> 对象需要完成四个步骤：  
  
1.  创建该维度对象并填充基本属性。  
  
     基本属性包括名称、维度类型、存储模式、数据源绑定、所有成员的属性名以及其他维度属性。  
  
     创建维度前，应确保该维度并不存在。 如果该维度已存在，则先将其删除，然后重新创建。  
  
2.  创建定义维度的各属性。  
  
     在使用每个属性之前都需将其添加到架构中（在示例代码的末尾查找 CreateDataItem 方法），然后才可将它们添加到该维度的属性集合中。  
  
     必须对每个属性定义键列和名称列。  
  
     维度的主键属性应定义为 AttributeUsage.Key 以明确说明此属性是该维度的键访问。  
  
3.  创建用户导航维度时所要访问的层次结构。  
  
     创建层次结构时，级别顺序是由从顶部到底部创建级别时所使用的顺序定义的。 最高级别是最先添加到层次结构的级别集合中的级别。  
  
4.  使用当前维度的 Update 方法更新服务器。  
  
 下面的示例代码创建示例数据库中的 Adventure Works products 表从产品维度。  
  
```  
static void CreateProductDimension(Database db, string datasourceName)  
{  
    // Create the Product dimension  
    Dimension dim = db.Dimensions.FindByName("Product");  
    if ( dim != null)  
       dim.Drop();  
    dim = db.Dimensions.Add("Product");  
    dim.Type = DimensionType.Products;  
    dim.UnknownMember = UnknownMemberBehavior.Hidden;  
    dim.AttributeAllMemberName = "All Products";  
    dim.Source = new DataSourceViewBinding(datasourceName);  
    dim.StorageMode = DimensionStorageMode.Molap;  
  
    #region Create attributes  
  
    DimensionAttribute attr;  
  
    attr = dim.Attributes.Add("Product Name");  
    attr.Usage = AttributeUsage.Key;  
    attr.Type = AttributeType.Product;  
    attr.OrderBy = OrderBy.Name;  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "EnglishProductName");  
  
    attr = dim.Attributes.Add("Product Line");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLine"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLineName");  
  
    attr = dim.Attributes.Add("Model Name");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ModelName"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Product Line"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Subcategory"));  
  
    attr = dim.Attributes.Add("Subcategory");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "ProductSubcategoryKey"));  
    attr.KeyColumns[0].NullProcessing = NullProcessing.UnknownMember;  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "EnglishProductSubcategoryName");  
    attr.AttributeRelationships.Add(new AttributeRelationship("Category"));  
  
    attr = dim.Attributes.Add("Category");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "ProductCategoryKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "EnglishProductCategoryName");  
  
    attr = dim.Attributes.Add("List Price");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ListPrice"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Size");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Size"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Weight");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Weight"));  
    attr.AttributeHierarchyEnabled = false;  
  
    #endregion  
  
    #region Create hierarchies  
  
    Hierarchy hier;  
  
    hier = dim.Hierarchies.Add("Product Model Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    hier = dim.Hierarchies.Add("Product Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Product Name";  
  
    hier = dim.Hierarchies.Add("Product Model Lines");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Product Line";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    #endregion  
  
    dim.Update();  
}  
  
static DataItem CreateDataItem(DataSourceView dsv, string tableName, string columnName)  
{  
    DataTable dataTable = ((DataSourceView)dsv).Schema.Tables[tableName];  
    DataColumn dataColumn = dataTable.Columns[columnName];  
    return new DataItem(tableName, columnName,  
        OleDbTypeConverter.GetRestrictedOleDbType(dataColumn.DataType));  
}  
  
```  
  
### <a name="processing-a-dimension"></a>处理维度  
 处理维度非常简单，使用 <xref:Microsoft.AnalysisServices.Dimension> 对象的 Process 方法即可。  
  
 处理某个维度会影响使用该维度的所有多维数据集。 有关处理选项的详细信息，请参阅[处理多维模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 以下代码对所提供数据库中的所有维度执行增量更新：  
  
```  
static void UpdateAllDimensions(Database db)  
{  
    foreach (Dimension dim in db.Dimensions)  
        dim.Process(ProcessType.ProcessUpdate);  
}  
```  
  
##  <a name="Cub"></a> 多维数据集对象  
 若要管理或处理多维数据集，需要对 <xref:Microsoft.AnalysisServices.Cube> 对象进行编程。  
  
### <a name="creating-dropping-and-finding-a-cube"></a>创建、删除和查找多维数据集  
 多维数据集的管理与维度的管理类似。 创建 <xref:Microsoft.AnalysisServices.Cube> 对象需要完成四个步骤：  
  
1.  创建该多维数据集对象并填充基本属性。  
  
     基本属性包括名称、存储模式、数据源绑定、默认度量值以及其他多维数据集属性。  
  
     创建多维数据集前，应确保该多维数据集并不存在。 在此示例中，如果该多维数据集已存在，则先将其删除，然后重新创建。  
  
2.  添加多维数据集的维度。  
  
     维度将添加到数据库的当前多维数据集维度集合中；多维数据集中的维度是对数据库维度集合的引用。 每个维度都必须分别映射到多维数据集。 在此示例中，映射维度时提供：数据库维度内部标识符、多维数据集中该维度的名称以及多维数据集中该命名维度的 ID。  
  
     在此示例代码中，请注意“Date”维度添加了三次，每次添加时使用不同的多维数据集维度名称：Date、Ship Date 和 Delivery Date。 这些维度也称为“角色扮演”维度。 它们的基维度是相同的 (Date)，但是在事实数据表中，该维度是用作不同的“角色”（Order Date、Ship Date、Delivery Date），请参阅本文档后面的“创建、删除和查找 MeasureGroup”以了解“角色扮演”维度是如何定义的。  
  
3.  创建用户浏览多维数据集的数据时所要访问的度量值组。  
  
     度量值组的创建将在本文档后面的“创建、删除和查找 MeasureGroup”中加以说明。 下面的示例使用不同的方法来包装度量值组的创建，一个度量值组使用一种方法。  
  
4.  使用当前多维数据集的 Update 方法更新服务器。  
  
     此 Update 方法将与更新选项 ExpandFull 一起使用，以确保在服务器中所有对象都完全更新。  
  
 下面的代码示例创建部分 Adventure Works 多维数据集。 该代码示例并不创建 Adventure Works Analysis Services 项目示例中包含的所有维度或度量值组。  
  
```  
static void CreateAdventureWorksCube(Database db, string datasourceName)  
{  
    // Create the Adventure Works cube  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    if ( cube != null)  
       cube.Drop();  
    db.Cubes.Add("Adventure Works");  
    cube.DefaultMeasure = "[Reseller Sales Amount]";  
    cube.Source = new DataSourceViewBinding(datasourceName);  
    cube.StorageMode = StorageMode.Molap;  
  
    #region Create cube dimensions  
  
    Dimension dim;  
  
    dim = db.Dimensions.GetByName("Date");  
    cube.Dimensions.Add(dim.ID, "Date", "Order Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Ship Date",  
        "Ship Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Delivery Date",  
        "Delivery Date Key - Dim Time");  
  
    dim = db.Dimensions.GetByName("Customer");  
    cube.Dimensions.Add(dim.ID);  
  
    dim = db.Dimensions.GetByName("Reseller");  
    cube.Dimensions.Add(dim.ID);  
    #endregion  
  
    #region Create measure groups  
  
    CreateSalesReasonsMeasureGroup(cube);  
    CreateInternetSalesMeasureGroup(cube);  
    CreateResellerSalesMeasureGroup(cube);  
    CreateCustomersMeasureGroup(cube);  
    CreateCurrencyRatesMeasureGroup(cube);  
  
    #endregion  
  
    cube.Update(UpdateOptions.ExpandFull);  
}  
```  
  
### <a name="processing-a-cube"></a>处理多维数据集  
 处理多维数据集非常简单，使用 <xref:Microsoft.AnalysisServices.Cube> 对象的 Process 方法即可。 处理多维数据集时还会处理该多维数据集中的所有度量值组以及这些度量值组中的所有分区。 在多维数据集中，只有分区是可以处理的对象；度量值组仅是为了处理而设的分区容器。 为多维数据集指定的处理类型会传播到分区。 对多维数据集和度量值组的处理在内部解析为对维度和分区的处理。  
  
 有关处理选项的详细信息，请参阅[处理对象&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)，和[处理多维模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 下面的代码对指定数据库中的所有多维数据集进行完整处理：  
  
```  
foreach (Cube cube in db.Cubes)  
             cube.Process(ProcessType.ProcessFull);  
     }  
```  
  
##  <a name="MG"></a> 度量值组对象  
 若要管理或处理度量值组，需要对 <xref:Microsoft.AnalysisServices.MeasureGroup> 对象进行编程。  
  
### <a name="creating-dropping-and-finding-a-measuregroup"></a>创建、删除和查找 MeasureGroup  
 度量值组的管理与维度和多维数据集的管理类似。 创建 <xref:Microsoft.AnalysisServices.MeasureGroup> 对象需要完成以下步骤：  
  
1.  创建该度量值组对象并填充基本属性。  
  
     基本属性包括名称、存储模式、处理模式、默认度量值以及其他度量值组属性。  
  
     创建度量值组前，应确保该度量值组并不存在。 在下面的示例代码中，如果该度量值组已存在，则先将其删除，然后重新创建。  
  
2.  创建度量值组的度量值。 对于创建的每个度量值，均会为其指定以下属性：名称、聚合函数、源列和格式字符串， 还可指定其他属性。 请注意，在下面的示例代码中，CreateDataItem 方法会向架构添加列。  
  
3.  添加度量值组的维度。  
  
4.  维度将添加到父多维数据集维度集合的当前度量值组维度集合中。 维度包含在度量值组维度集合中后，事实数据表中的键列便可映射至该维度，从而可以通过该维度来浏览度量值组。  
  
     在下面的示例代码中，请参阅“Mapping dimension and key column from fact table”下面的行。 角色扮演维度是通过将不同的代理键链接到使用不同名称的同一维度来实现的。 对于每一角色扮演维度（Date、Ship Date、Delivery Date），有不同的代理键与其链接（OrderDateKey、ShipDateKey、DueDateKey）。 所有这些键都来自事实数据表 FactInternetSales。  
  
5.  添加度量值组的已设计分区。  
  
     在下面的示例代码中，分区的创建包装在一个方法中。  
  
6.  使用当前度量值组的 Update 方法更新服务器。  
  
     在下面的示例代码中，更新相应的多维数据集时将更新所有度量值组。  
  
 下面的示例代码将创建 Adventure Works Analysis Services 项目示例的 InternetSales 度量值组。  
  
```  
static void CreateInternetSalesMeasureGroup(Cube cube)  
{  
    // Create the Internet Sales measure group  
    Database db = cube.Parent;  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Internet Sales");  
    if ( mg != null)  
       mg.Drop();  
    mg = cube.MeasureGroups.Add("Internet Sales");  
    mg.StorageMode = StorageMode.Molap;  
    mg.ProcessingMode = ProcessingMode.LazyAggregations;  
    mg.Type = MeasureGroupType.Sales;  
  
    #region Create measures  
  
    Measure meas;  
  
    meas = mg.Measures.Add("Internet Sales Amount");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesAmount");  
  
    meas = mg.Measures.Add("Internet Order Quantity");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderQuantity");  
  
    meas = mg.Measures.Add("Internet Unit Price");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Visible = false;  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "UnitPrice");  
  
    meas = mg.Measures.Add("Internet Total Product Cost");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    //meas.MeasureExpression = "[Internet Total Product Cost] * [Average Rate]";  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "TotalProductCost");  
  
    meas = mg.Measures.Add("Internet Order Count");  
    meas.AggregateFunction = AggregationFunction.Count;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey");  
  
    #endregion  
  
    #region Create measure group dimensions  
  
    CubeDimension cubeDim;  
    RegularMeasureGroupDimension regMgDim;  
    ManyToManyMeasureGroupDimension mmMgDim;  
    MeasureGroupAttribute mgAttr;  
  
    //   Mapping dimension and key column from fact table  
    //      > select dimension and add it to the measure group  
    cubeDim = cube.Dimensions.GetByName("Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
  
    //      > add key column from dimension and map it with   
    //        the surrogate key in the fact table  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);   // this is dimension key column  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderDateKey"));   // this surrogate key in fact table  
  
    cubeDim = cube.Dimensions.GetByName("Ship Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ShipDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Delivery Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "DueDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Customer");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Full Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CustomerKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Product");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Product Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Source Currency");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Currency").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CurrencyKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Sales Reason");  
    mmMgDim = new ManyToManyMeasureGroupDimension();  
    mmMgDim.CubeDimensionID = cubeDim.ID;  
    mmMgDim.MeasureGroupID = cube.MeasureGroups.GetByName("Sales Reasons").ID;  
    mg.Dimensions.Add(mmMgDim);  
  
    cubeDim = cube.Dimensions.GetByName("Internet Sales Order Details");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Sales Order Key").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderNumber"));  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderLineNumber"));  
  
    #endregion  
  
    #region Create partitions  
  
    CreateInternetSalesMeasureGroupPartitions( mg)  
  
    #endregion  
}  
```  
  
### <a name="processing-a-measure-group"></a>处理度量值组  
 处理度量值组非常简单，使用 <xref:Microsoft.AnalysisServices.MeasureGroup> 对象的 Process 方法即可。 处理度量值组时将处理属于该度量值组的所有分区。 对度量值组的处理在内部解析为对维度和分区的处理。 请参阅[处理分区](#ProcPart)本文档中。  
  
 有关处理选项的详细信息，请参阅[处理对象&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)，和[处理多维模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 下面的代码将对提供的多维数据集中的所有度量值组进行完整处理。  
  
```  
static void FullProcessAllMeasureGroups(Cube cube)  
{  
    foreach (MeasureGroup mg in cube.MeasureGroups)  
        mg.Process(ProcessType.ProcessFull);  
}  
```  
  
##  <a name="Part"></a> 分区对象  
 若要管理或处理分区，需要对 <xref:Microsoft.AnalysisServices.Partition> 对象进行编程。  
  
### <a name="creating-dropping-and-finding-a-partition"></a>创建、删除和查找分区  
 分区是一种简单的对象，只需两个步骤即可创建。  
  
1.  创建分区对象并填充基本属性。  
  
     基本属性包括名称、存储模式、分区源、切片以及其他度量值组属性。 分区源定义当前分区的 SQL SELECT 语句。 切片是一个 MDX 表达式，用于指定从包含在当前分区中的父度量值组中分隔一部分维度的元组或集。 对于 MOLAP 分区，切片是每次处理分区时自动确定的。  
  
     创建分区前，应确保该分区并不存在。 在下面的示例代码中，如果该分区已存在，则先将其删除，然后重新创建。  
  
2.  使用当前分区的 Update 方法更新服务器。  
  
     在下面的示例代码中，更新相应的多维数据集时将更新所有分区。  
  
 下面的代码示例为“InternetSales”度量值组创建分区。  
  
```  
static void CreateInternetSalesMeasureGroupPartitions(MeasureGroup mg)  
{  
    Partition part;  
    part = mg.Partitions.FindByName("Internet_Sales_184");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_184");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey <= '184'");  
    part.Slice = "[Date].[Calendar Year].&[2001]";  
    part.Annotations.Add("LastOrderDateKey", "184");  
  
    part = mg.Partitions.FindByName("Internet_Sales_549");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_549");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '184' AND OrderDateKey <= '549'");  
    part.Slice = "[Date].[Calendar Year].&[2002]";  
    part.Annotations.Add("LastOrderDateKey", "549");  
  
    part = mg.Partitions.FindByName("Internet_Sales_914");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_914");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '549' AND OrderDateKey <= '914'");  
    part.Slice = "[Date].[Calendar Year].&[2003]";  
    part.Annotations.Add("LastOrderDateKey", "914");  
}  
```  
  
###  <a name="ProcPart"></a> 处理分区  
 处理分区非常简单，使用 <xref:Microsoft.AnalysisServices.Partition> 对象的 Process 方法即可。  
  
 有关处理选项的详细信息，请参阅[处理对象&#40;XMLA&#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)和[处理多维模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 下面的代码示例对指定度量值组中的所有分区进行完整处理。  
  
```  
static void FullProcessAllPartitions(MeasureGroup mg)  
{  
    foreach (Partition part in mg.Partitions)  
        part.Process(ProcessType.ProcessFull);  
}  
```  
  
### <a name="merging-partitions"></a>合并分区  
 合并分区指的是执行任何使两个或两个以上分区成为一个分区的操作。  
  
 合并分区是 <xref:Microsoft.AnalysisServices.Partition> 对象的一个方法。 此命令将一个或多个源分区的数据合并到一个目标分区中，然后删除源分区。  
  
 只有符合下列所有条件的分区才能合并：  
  
-   这些分区位于同一度量值组中。  
  
-   这些分区都以相同的模式（MOLAP、HOLAP 和 ROLAP）存储。  
  
-   这些分区驻留在同一服务器上；同一服务器上的远程分区可以合并。  
  
 与早期版本中，不同中[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]不需要所有源分区都具有相同的聚合设计。  
  
 为目标分区生成的聚合集与运行合并命令前的聚合集相同。  
  
 下面的代码示例合并指定度量值组中的所有分区。 这些分区合并到该度量值组的第一个分区。  
  
```  
static void MergeAllPartitions(MeasureGroup mg)  
{  
    if (mg.Partitions.Count > 1)  
    {  
        Partition[] partArray = new Partition[mg.Partitions.Count - 1];  
        for (int i = 1; i < mg.Partitions.Count; i++)  
            partArray[i - 1] = mg.Partitions[i];  
        mg.Partitions[0].Merge(partArray);  
        //To have last changes in the server reflected in AMO  
        mg.Refresh();  
    }  
```  
  
##  <a name="AD"></a> 聚合对象  
 若要设计一个聚合并将其应用于一个或多个分区，需要对 <xref:Microsoft.AnalysisServices.Aggregation> 对象进行编程。  
  
### <a name="creating-and-dropping-aggregations"></a>创建和删除聚合  
 创建聚合并将其分配给度量值组或分区的过程非常简单，使用 <xref:Microsoft.AnalysisServices.AggregationDesign> 对象的 DesignAggregations 方法即可。 <xref:Microsoft.AnalysisServices.AggregationDesign> 对象是独立于分区的对象，<xref:Microsoft.AnalysisServices.AggregationDesign> 对象包含在 <xref:Microsoft.AnalysisServices.MeasureGroup> 对象中。 可以将聚合设计为达到指定的优化级别（0 至 100）或者达到指定的存储级别（字节）。 多个分区可以使用相同的聚合设计。  
  
 下面的代码示例为所提供度量值组中的所有分区创建聚合。 分区中的所有现有聚合都将被删除。  
  
```  
static public String DesignAggregationsOnPartitions(MeasureGroup mg, double optimizationWanted, double maxStorageBytes)  
{  
    double optimization = 0;  
    double storage = 0;  
    long aggCount = 0;  
    bool finished = false;  
    AggregationDesign ad = null;  
    String aggDesignName;  
    String AggregationsDesigned = "";  
    aggDesignName = mg.AggregationPrefix + "_" + mg.Name;  
    ad = mg.AggregationDesigns.Add();  
    ad.Name = aggDesignName;  
    ad.InitializeDesign();  
    while ((!finished) && (optimization < optimizationWanted) && (storage < maxStorageBytes))  
    {  
        ad.DesignAggregations(out optimization, out storage, out aggCount, out finished);  
    }  
    ad.FinalizeDesign();  
    foreach (Partition part in mg.Partitions)  
    {  
        part.AggregationDesignID = ad.ID;  
        AggregationsDesigned += aggDesignName + " = " + aggCount.ToString() + " aggregations designed\r\n\tOptimization: " + optimization.ToString() + "/" + optimizationWanted.ToString() + "\n\r\tStorage: " + storage.ToString() + "/" + maxStorageBytes.ToString() + " ]\n\r";  
     }  
     return AggregationsDesigned;  
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
  
  
