---
title: 第 3 课：处理自行车购买者挖掘结构 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e748c2cd-339d-4e82-82f1-be2d0fc41b61
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2e3f85016b32884b9a6b809e28d20d9985f97cd9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62655793"
---
# <a name="lesson-3-processing-the-bike-buyer-mining-structure"></a>第 3 课：处理自行车购买者挖掘结构
  在本课程中，您将使用 INSERT INTO 语句和 vTargetMail 视图，从[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]示例数据库来处理挖掘结构和挖掘模型中创建[第 1 课：创建自行车购买者挖掘结构](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md)和[第 2 课：向自行车购买者挖掘结构添加挖掘模型](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)。  
  
 处理挖掘结构时，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将读取源数据并生成支持挖掘模型的结构。 处理挖掘模型时，挖掘结构定义的数据将通过所选择的数据挖掘算法进行传递。 该算法将搜索趋势和模式，然后在挖掘模型中存储此信息。 因此，挖掘模型不包含实际源数据，而是包含由算法发现的信息。 有关处理挖掘模型的详细信息，请参阅[处理要求和注意事项&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 仅在更改了结构列或源数据的情况下，才需要重新处理挖掘结构。 如果将挖掘模型添加到已处理的挖掘结构中，则可使用 INSERT INTO MINING MODEL 语句定型新的挖掘模型。  
  
## <a name="train-structure-template"></a>定型结构模板  
 为了定型挖掘结构及其关联的挖掘模型，请使用[INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx)语句。 可以将语句中的代码分为下列几部分：  
  
-   标识挖掘结构  
  
-   列出挖掘结构中的列  
  
-   定义定型数据  
  
 下面是 INSERT INTO 语句的一般示例：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 代码的第一行标识将定型的挖掘结构：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 代码的第二行指定由挖掘结构定义的列。 必须列出挖掘结构的每一列，并且每列必须映射到源查询数据所包含的对应列。  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 代码的最后一行定义将用于定型挖掘结构的数据：  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 在本课中，您将使用 `OPENQUERY` 来定义源数据。 定义源查询的其他方法的信息，请参阅[&#60;源数据查询&#62;](/sql/dmx/source-data-query)。  
  
## <a name="lesson-tasks"></a>课程任务  
 在本课程中，将执行以下任务：  
  
-   处理自行车购买者挖掘结构  
  
## <a name="processing-the-predictive-mining-structure"></a>处理预测性挖掘结构  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>使用 INSERT INTO 处理挖掘结构  
  
1.  在中**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  将 INSERT INTO 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    [<mining structure name>]   
    ```  
  
     使用：  
  
    ```  
    Bike Buyer  
    ```  
  
4.  将  
  
    ```  
    <mining structure columns>  
    ```  
  
     使用：  
  
    ```  
    [Customer Key],  
    [Age],  
    [Bike Buyer],  
    [Commute Distance],  
    [Education],  
    [Gender],  
    [House Owner Flag],  
    [Marital Status],  
    [Number Cars Owned],  
    [Number Children At Home],  
    [Occupation],  
    [Region],  
    [Total Children],  
    [Yearly Income]  
    ```  
  
5.  将  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     使用：  
  
    ```  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
     OPENQUERY 语句将引用 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 数据源，以访问 vTargetMail 视图。 该视图包含将用于定型挖掘模型的源数据。  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    INSERT INTO MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key],  
       [Age],  
       [Bike Buyer],  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]     
    )  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
6.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
7.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`Process Bike Buyer Structure.dmx`。  
  
8.  在工具栏上，单击**Execute**按钮。  
  
 在下一课中，您将浏览在本课中向挖掘结构添加的挖掘模型中的内容。  
  
## <a name="next-lesson"></a>下一课  
 [第 4 课：浏览自行车购买者挖掘模型](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
  
  
