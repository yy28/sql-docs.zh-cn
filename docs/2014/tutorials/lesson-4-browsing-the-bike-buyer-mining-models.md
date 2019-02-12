---
title: 第 4 课：浏览自行车购买者挖掘模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8de3c500-f881-42da-a096-b6c03300d58d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 709df371d840d4b24e420b4fcd08750fd31e8075
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011526"
---
# <a name="lesson-4-browsing-the-bike-buyer-mining-models"></a>第 4 课：浏览自行车购买者挖掘模型
  在本课程中，您将使用[SELECT (DMX)](/sql/dmx/select-dmx)语句浏览决策树和聚类分析挖掘中的内容模型中创建的[第 2 课：向预测性挖掘结构添加挖掘模型](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)。  
  
 挖掘模型中包含的列不是由挖掘结构定义的列，而是用于说明通过算法获得的趋势和模式的特定列集。 描述了这些挖掘模型列[DMSCHEMA_MINING_MODEL_CONTENT 行集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)架构行集。 例如，内容架构行集中的 MODEL_NAME 列包含挖掘模型的名称。 对于聚类分析挖掘模型，NODE_CAPTION 列包含每个分类的名称，NODE_DESCRIPTION 列包含每个分类的特征说明。 您可以通过使用 SELECT FROM 浏览这些列\<模型 >。在 DMX 中的内容语句。 也可以使用该语句浏览用于创建挖掘模型的数据。 为了使用该语句，必须对挖掘结构启用钻取功能。 有关语句的详细信息，请参阅[SELECT FROM&#60;模型&#62;。用例&#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx)。  
  
 也可以使用 SELECT DISTINCT 语句返回离散列的所有状态。 例如，如果对 gender 列执行此操作，则查询将返回 `male` 和 `female`。  
  
## <a name="lesson-tasks"></a>课程任务  
 在本课程中，将执行以下任务：  
  
-   浏览挖掘模型中包含的内容  
  
-   返回源数据中用于为挖掘模型定型的事例  
  
-   浏览其他可用于特定离散列的状态  
  
## <a name="returning-the-content-of-a-mining-model"></a>返回挖掘模型的内容  
 在本课程中，您使用[SELECT FROM&#60;模型&#62;。内容&#40;DMX&#41; ](/sql/dmx/select-from-model-dimension-content-dmx)语句返回聚类分析模型的内容。  
  
 下面是 SELECT FROM 的一般示例\<模型 >。内容的语句：  
  
```  
SELECT <select list> FROM [<mining model>].CONTENT  
WHERE <where clause>  
```  
  
 代码的第一行定义各列从挖掘模型内容以及与列关联的挖掘模型中返回：  
  
```  
SELECT <select list> FROM [<mining model].CONTENT  
```  
  
 挖掘模型名称旁边的 .CONTENT 子句指定将要返回挖掘模型的内容。 有关挖掘模型中包含的列的详细信息，请参阅[DMSCHEMA_MINING_MODEL_CONTENT 行集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)。  
  
 您可以选择性地使用代码的最后一行筛选该语句返回的结果：  
  
```  
WHERE <where clause>  
```  
  
 例如，如果要将查询结果仅限制为包含大量事例的分类，则需要将以下 WHERE 子句添加到 SELECT 语句：  
  
```  
WHERE NODE_SUPPORT > 100  
```  
  
 有关使用 WHERE 语句的详细信息，请参阅[选择&#40;DMX&#41;](/sql/dmx/select-dmx)。  
  
#### <a name="to-return-the-content-of-the-clustering-mining-model"></a>返回聚类分析挖掘模型的内容  
  
1.  在中**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  SELECT from 的一般示例复制\<模型 >。内容到空白查询语句。  
  
3.  将  
  
    ```  
    <select list>   
    ```  
  
     使用：  
  
    ```  
    *  
    ```  
  
     也可以替换 * 与任意中包含的列的列表[DMSCHEMA_MINING_MODEL_CONTENT 行集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)。  
  
4.  将  
  
    ```  
    [<mining model>]   
    ```  
  
     使用：  
  
    ```  
    [Clustering]  
    ```  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    SELECT * FROM [Clustering].CONTENT  
    ```  
  
5.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
6.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`SELECT_CONTENT.dmx`。  
  
7.  在工具栏上，单击**Execute**按钮。  
  
     查询返回挖掘模型的内容。  
  
## <a name="use-drillthrough"></a>使用钻取功能  
 下一步将使用钻取语句返回用于为决策树挖掘模型定型的事例抽样。 在本课程中，您使用[SELECT FROM&#60;模型&#62;。用例&#40;DMX&#41; ](/sql/dmx/select-from-model-content-dmx)语句返回决策树模型的内容。  
  
 下面是 SELECT FROM 的一般示例\<模型 >。用例语句：  
  
```  
SELECT <select list>   
FROM [<mining model>].CASES  
WHERE IsInNode('<node id>')  
```  
  
 代码的第一行定义从源数据返回的列和这些列所包含的挖掘模型：  
  
```  
SELECT <select list> FROM [<mining model>].CASES  
```  
  
 .CASES 子句指定您正在执行钻取查询。 为了使用钻取功能，您必须在创建挖掘模型时启用该功能。  
  
 代码的最后一行可选，该行指定了要从中请求事例的挖掘模型中的节点：  
  
```  
WHERE IsInNode('<node id>')  
```  
  
 有关使用带有 IsInNode 的 WHERE 语句的详细信息，请参阅[SELECT FROM&#60;模型&#62;。用例&#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx)。  
  
#### <a name="to-return-the-cases-that-were-used-to-train-the-mining-model"></a>返回用于为挖掘模型定型的事例  
  
1.  在中**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  SELECT from 的一般示例复制\<模型 >。到空白查询的情况下语句。  
  
3.  将  
  
    ```  
    <select list>   
    ```  
  
     使用：  
  
    ```  
    *  
    ```  
  
     您还可以使用源数据（如 [自行车购买者]）中包含的任意列的列表替换 *。  
  
4.  将  
  
    ```  
    [<mining model>]   
    ```  
  
     使用：  
  
    ```  
    [Decision Tree]  
    ```  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    SELECT *   
    FROM [Decision Tree].CASES  
    ```  
  
5.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
6.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`SELECT_DRILLTHROUGH.dmx`。  
  
7.  在工具栏上，单击**Execute**按钮。  
  
     查询返回用于为决策树挖掘模型定型的源数据。  
  
## <a name="return-the-states-of-a-discrete-mining-model-column"></a>返回离散挖掘模型列的状态  
 下一步将使用 SELECT DISTINCT 语句返回指定的挖掘模型列的各种可能状态。  
  
 下面是 SELECT DISTINCT 语句的一般示例：  
  
```  
SELECT DISTINCT [<column>]   
FROM [<mining model>]  
```  
  
 代码的第一行定义了为其返回状态的挖掘模型列：  
  
```  
SELECT DISTINCT [<column>]   
```  
  
 必须包括 DISTINCT 才能返回列的所有状态。 如果排除 DISTINCT，则整个语句会变为预测的快捷方式并且返回指定列最可能的状态。 有关详细信息，请参阅 [SELECT (DMX)](/sql/dmx/select-dmx)。  
  
#### <a name="to-return-the-states-of-a-discrete-column"></a>返回离散列的状态  
  
1.  在中**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  将 SELECT Distinct 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    [<column,name>   
    ```  
  
     使用：  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  将  
  
    ```  
    [<mining model>]   
    ```  
  
     使用：  
  
    ```  
    [Decision Tree]  
    ```  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    SELECT DISTINCT [Bike Buyer]   
    FROM [Decision Tree]  
    ```  
  
5.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
6.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`SELECT_DISCRETE.dmx`。  
  
7.  在工具栏上，单击**Execute**按钮。  
  
     查询返回 Bike Buyer 列的可能状态。  
  
 在下一课中，您将使用决策树挖掘模型预测潜在的客户是否为自行车购买者。  
  
## <a name="next-lesson"></a>下一课  
 [第 5 课：执行预测查询](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
  
  
