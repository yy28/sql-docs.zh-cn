---
title: 第1课：创建自行车购买者挖掘结构 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a73ac60b-660f-458a-bd2f-993fbeba7226
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d6384910858d87a80aa3c8f897bc88e45f4504fb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62678499"
---
# <a name="lesson-1-creating-the-bike-buyer-mining-structure"></a>第 1 课：创建自行车购买者挖掘结构
  在本课中，将创建一个挖掘结构，可以使用该结构预测 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的潜在客户是否会购买自行车。 如果不熟悉挖掘结构及其在数据挖掘中的角色，请参阅[挖掘结构 &#40;Analysis Services 数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)。  
  
 您将在本课中创建的自行车购买者挖掘结构支持根据[Microsoft 聚类分析算法](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)[Microsoft 决策树算法](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)添加挖掘模型。 在后面的课程中，您将使用聚类分析挖掘模型来浏览各种客户分组方式，并使用决策树挖掘模型来预测潜在的客户是否将购买自行车。  
  
## <a name="create-mining-structure-statement"></a>CREATE 挖掘 STRUCTURE 语句  
 若要创建挖掘结构，请使用[CREATE 挖掘 structure &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)语句。 可以将语句中的代码分为下列几部分：  
  
-   命名结构。  
  
-   定义键列。  
  
-   定义挖掘列。  
  
-   定义可选的测试数据集。  
  
 下面是 CREATE MINING STRUCTURE 语句的一般示例：  
  
```  
CREATE MINING STRUCTURE [<mining structure name>]  
(  
    <key column>,  
    <mining structure columns>  
)   
WITH HOLDOUT (<holdout specifier>)  
```  
  
 代码的第一行定义了结构的名称：  
  
```  
CREATE MINING STRUCTURE [<mining structure name>]  
```  
  
 有关在数据挖掘扩展插件（DMX）中命名对象的信息，请参阅[标识符 &#40;DMX&#41;](/sql/dmx/identifiers-dmx)。  
  
 代码的下一行定义了挖掘结构的键列，它唯一标识源数据中的实体：  
  
```  
<key column>,  
```  
  
 在将要创建的挖掘结构中，客户标识符 `CustomerKey` 定义了源数据中的实体。  
  
 代码的下一行用于定义与挖掘结构关联的挖掘模型所使用的挖掘列：  
  
```  
<mining structure columns>  
```  
  
 使用以下语法，可以在挖掘\<结构列> 中使用离散化函数来离散化连续列：  
  
 `DISCRETIZE(<method>,<number of buckets>)`  
  
 有关离散化列的详细信息，请参阅[数据挖掘&#41;&#40;离散化方法](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md)。 有关您可以定义的挖掘结构列类型的详细信息，请参阅[挖掘结构列](../../2014/analysis-services/data-mining/mining-structure-columns.md)。  
  
 最后一行代码定义挖掘结构中的可选分区：  
  
```  
WITH HOLDOUT (<holdout specifier>)  
```  
  
 您要指定某些数据用于测试与该结构相关的挖掘模型，剩余数据用于定型该模型。 默认情况下，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 创建的测试数据集包含所有事例数据的 30%。 您将添加这样一个说明：测试数据集应包含 30% 的事例，并且最多可以包含 1000 个事例。 如果 30% 的事例不足 1000 个，则测试数据集将包含较小数量的事例。  
  
## <a name="lesson-tasks"></a>课程任务  
 您将在本课中执行以下任务：  
  
-   创建新的空白查询。  
  
-   更改查询以创建挖掘结构。  
  
-   执行查询。  
  
## <a name="creating-the-query"></a>创建查询  
 第一步是连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例，并在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中创建一个新的 DMX 查询。  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中创建一个新的 DMX 查询  
  
1.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  在 "**连接到服务器**" 对话框中，选择 "**服务器类型**" **Analysis Services**。 在 "**服务器名称**" `LocalHost`中，键入或键入要为本课连接[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]到的实例的名称。 单击“连接”  。  
  
3.  在**对象资源管理器** [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中，右键单击实例，指向 "**新建查询**"，然后单击 " **DMX** "，打开**查询编辑器**和一个新的空白查询。  
  
## <a name="altering-the-query"></a>更改查询  
 第二步是修改上述 CREATE MINING STRUCTURE 语句以创建自行车购买者挖掘结构。  
  
#### <a name="to-customize-the-create-mining-structure-statement"></a>自定义 CREATE MINING STRUCTURE 语句  
  
1.  在查询编辑器中，将 CREATE MINING STRUCTURE 语句的一般示例复制到空白查询中。  
  
2.  将  
  
    ```  
    [<mining structure>]   
    ```  
  
     替换为：  
  
    ```  
    [Bike Buyer]  
    ```  
  
3.  将  
  
    ```  
    <key column>   
    ```  
  
     替换为：  
  
    ```  
    CustomerKey LONG KEY  
    ```  
  
4.  将  
  
    ```  
    <mining structure columns>   
    ```  
  
     替换为：  
  
    ```  
    [Age] LONG DISCRETIZED(Automatic,10),  
    [Bike Buyer] LONG DISCRETE,  
    [Commute Distance] TEXT DISCRETE,  
    [Education] TEXT DISCRETE,  
    [Gender] TEXT DISCRETE,  
    [House Owner Flag] TEXT DISCRETE,  
    [Marital Status] TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Number Children At Home] LONG DISCRETE,  
    [Occupation] TEXT DISCRETE,  
    [Region] TEXT DISCRETE,  
    [Total Children]LONG DISCRETE,  
    [Yearly Income] DOUBLE CONTINUOUS  
    ```  
  
5.  将  
  
    ```  
    WITH HOLDOUT (holdout specifier>)  
    ```  
  
     替换为：  
  
    ```  
    WITH HOLDOUT (30 PERCENT or 1000 CASES)  
    ```  
  
     现在，完整的挖掘结构语句应该如下所示：  
  
    ```  
    CREATE MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key] LONG KEY,  
       [Age]LONG DISCRETIZED(Automatic,10),  
       [Bike Buyer] LONG DISCRETE,  
       [Commute Distance] TEXT DISCRETE,  
       [Education] TEXT DISCRETE,  
       [Gender] TEXT DISCRETE,  
       [House Owner Flag] TEXT DISCRETE,  
       [Marital Status] TEXT DISCRETE,  
       [Number Cars Owned]LONG DISCRETE,  
       [Number Children At Home]LONG DISCRETE,  
       [Occupation] TEXT DISCRETE,  
       [Region] TEXT DISCRETE,  
       [Total Children]LONG DISCRETE,  
       [Yearly Income] DOUBLE CONTINUOUS  
    )  
    WITH HOLDOUT (30 PERCENT or 1000 CASES)  
  
    ```  
  
6.  在 "**文件**" 菜单上，单击 "**将 DMXQuery1 另存为**"。  
  
7.  在 "**另存为**" 对话框中，浏览到相应的文件夹，并将`Bike Buyer Structure.dmx`该文件命名为。  
  
## <a name="executing-the-query"></a>执行查询  
 最后一步是执行查询。 创建并保存查询后，需要执行查询。 也就是说，需要运行查询语句以便在服务器上创建挖掘结构。 有关在查询编辑器中执行查询的详细信息，请参阅[SQL Server Management Studio&#41;数据库引擎查询编辑器 &#40;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)。  
  
#### <a name="to-execute-the-query"></a>执行查询  
  
1.  在查询编辑器中，单击工具栏上的 "**执行**"。  
  
     语句执行完毕后，查询的状态将显示在查询编辑器底部的 "**消息**" 选项卡中。 所显示的消息应为：  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     名为 "**自行车购买**者" 的新结构现在存在于服务器上。  
  
 在下一课中，您将向刚才创建的结构中添加挖掘模型。  
  
## <a name="next-lesson"></a>下一课  
 [第 2 课：向自行车购买者挖掘结构添加挖掘模型](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)  
  
  
