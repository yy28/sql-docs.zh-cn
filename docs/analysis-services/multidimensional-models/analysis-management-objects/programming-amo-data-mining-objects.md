---
title: 编程 AMO 数据挖掘对象 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9ba64d48fe93ea047210c00717d84cde0e4dcae9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="programming-amo-data-mining-objects"></a>AMO 数据挖掘对象的编程
  使用 AMO 对数据挖掘对象进行编程非常简单直接。 第一步是创建数据结构模型以支持挖掘项目。 然后创建数据挖掘模型，该模型支持您要用于预测或查找数据下未看到的关系的挖掘算法。 创建挖掘项目（包括结构和算法）后，可以处理挖掘模型以获取定型的模型，稍后从客户端应用程序进行查询和预测时将使用该模型。  
  
 请记住 AMO 不用于查询，而是用于管理挖掘结构和模型。 若要查询你的数据，使用[使用 ADOMD.NET 开发](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
 本主题包含以下各节：  
  
-   [MiningStructure 对象](#MiningStructure)  
  
-   [MiningModel 对象](#MiningModel)  
  
##  <a name="MiningStructure"></a> MiningStructure 对象  
 挖掘结构是用于创建所有挖掘模型的数据结构的定义。 挖掘结构包含与数据库中定义的数据源视图的绑定，以及组成挖掘模型的所有列的定义。 一个挖掘结构可包含多个挖掘模型。  
  
 创建 <xref:Microsoft.AnalysisServices.MiningStructure> 对象需要执行下列步骤：  
  
1.  创建 <xref:Microsoft.AnalysisServices.MiningStructure> 对象并填充基本属性。 这些基本属性包括对象名称、对象 ID（内部标识）和数据源绑定。  
  
2.  创建模型的列。 列可以为标量，也可以为表定义。  
  
     每一列都需要名称、内部 ID、类型、内容定义和绑定。  
  
3.  使用 <xref:Microsoft.AnalysisServices.MiningStructure> 对象的 Update 方法将该对象更新到服务器。  
  
     可对挖掘结构进行处理，处理挖掘结构时，会对子挖掘模型进行处理和重新定型。  
  
 下面的示例代码创建挖掘结构来预测一段时序中的销售情况。 运行示例代码之前，确保数据库*db*作为参数传递`CreateSalesForecastingMiningStructure`，包含在`db.DataSourceViews[0]`对视图的引用*dbo.vTimeSeries*中[!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]示例数据库。  
  
```  
public static MiningStructure CreateSalesForecastingMiningStructure(Database db)  
{  
    MiningStructure ms = db.MiningStructures.FindByName("Forecasting Sales Structure");  
    if (ms != null)  
        ms.Drop();  
    ms = db.MiningStructures.Add("Forecasting Sales Structure", "Forecasting Sales Structure");  
    ms.Source = new DataSourceViewBinding(db.DataSourceViews[0].ID);  
  
    ScalarMiningStructureColumn amount = ms.Columns.Add("Amount", "Amount");  
    amount.Type = MiningStructureColumnTypes.Double;  
    amount.Content = MiningStructureColumnContents.Continuous;  
    amount.KeyColumns.Add("vTimeSeries", "Amount", OleDbType.Currency);  
  
    ScalarMiningStructureColumn modelRegion = ms.Columns.Add("Model Region", "Model Region");  
    modelRegion.IsKey = true;  
    modelRegion.Type = MiningStructureColumnTypes.Text;  
    modelRegion.Content = MiningStructureColumnContents.Key;  
    modelRegion.KeyColumns.Add("vTimeSeries", "ModelRegion", OleDbType.WChar, 56);  
  
    ScalarMiningStructureColumn qty = ms.Columns.Add("Quantity", "Quantity");  
    qty.Type = MiningStructureColumnTypes.Long;  
    qty.Content = MiningStructureColumnContents.Continuous;  
    qty.KeyColumns.Add("vTimeSeries", "Quantity", OleDbType.Integer);  
  
    ScalarMiningStructureColumn timeIndex = ms.Columns.Add("TimeIndex", "TimeIndex");  
    timeIndex.IsKey = true;  
    timeIndex.Type = MiningStructureColumnTypes.Long;  
    timeIndex.Content = MiningStructureColumnContents.KeyTime;  
    timeIndex.KeyColumns.Add("vTimeSeries", "TimeIndex", OleDbType.Integer);  
  
    ms.Update();  
    return ms;  
}  
```  
  
##  <a name="MiningModel"></a> MiningModel 对象  
 挖掘模型是将在挖掘算法中使用的所有列和列定义的存储库。  
  
 创建 <xref:Microsoft.AnalysisServices.MiningModel> 对象需要执行下列步骤：  
  
1.  创建 <xref:Microsoft.AnalysisServices.MiningModel> 对象并填充基本属性。  
  
     这些基本属性包括对象名称、对象 ID（内部标识）和挖掘算法规范。  
  
2.  添加挖掘模型的列。 必须将其中一列定义为事例键。  
  
3.  使用 <xref:Microsoft.AnalysisServices.MiningModel> 对象的 Update 方法将该对象更新到服务器。  
  
     <xref:Microsoft.AnalysisServices.MiningModel> 对象的处理可以独立于父 <xref:Microsoft.AnalysisServices.MiningStructure> 中的其他模型。  
  
 下面的示例代码基于“Forecasting Sales Structure”挖掘结构创建 Microsoft 时序预测模型：  
  
```  
public static MiningModel CreateSalesForecastingMiningModel(MiningStructure ms)  
{  
    if (ms.MiningModels.ContainsName("Sales Forecasting Model"))  
    {  
        ms.MiningModels["Sales Forecasting Model"].Drop();  
    }  
    MiningModel mm = ms.CreateMiningModel(true, "Sales Forecasting Model");  
    mm.Algorithm = MiningModelAlgorithms.MicrosoftTimeSeries;  
    mm.AlgorithmParameters.Add("PERIODICITY_HINT", "{12}");  
  
    MiningModelColumn amount = new MiningModelColumn();  
    amount.SourceColumnID = "Amount";  
    amount.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn modelRegion = new MiningModelColumn();  
    modelRegion.SourceColumnID = "Model Region";  
    modelRegion.Usage = MiningModelColumnUsages.Key;  
  
    MiningModelColumn qty = new MiningModelColumn();  
    qty.SourceColumnID = "Quantity";  
    qty.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn ti = new MiningModelColumn();  
    ti.SourceColumnID = "TimeIndex";  
    ti.Usage = MiningModelColumnUsages.Key;  
  
    mm.Update();  
    mm.Process(ProcessType.ProcessFull);  
    return mm;  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices>   
 [AMO 基础类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)   
 [引入 AMO 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO 数据挖掘类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)   
 [逻辑体系结构 & #40;Analysis Services-多维数据 & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象 & #40;Analysis Services-多维数据 & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
