---
title: 第 3 课：处理市场篮挖掘结构 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 095a043f-cf6f-45bb-a021-ae4e1b535c65
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ce2c2e6944d524a38edc331d2cd128ca7cf7d419
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56018259"
---
# <a name="lesson-3-processing-the-market-basket-mining-structure"></a>第 3 课：处理市场篮挖掘结构
  在本课程中，您将使用[INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx)语句的 vAssocSeqLineItems 和 vAssocSeqOrders 从[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]示例数据库来处理挖掘结构和挖掘模型在中创建[第 1 课：创建市场篮挖掘结构](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)和[第 2 课：向市场篮挖掘结构添加挖掘模型](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)。  
  
 处理挖掘结构时，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将读取源数据并生成支持挖掘模型的结构。 处理挖掘模型，挖掘结构定义的数据将通过所选的数据挖掘算法。 该算法将搜索趋势和模式，然后在挖掘模型中存储此信息。 因此，挖掘模型不包含实际源数据，而是包含由算法发现的信息。 有关处理挖掘模型的详细信息，请参阅[处理要求和注意事项&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 如果更改了结构列或源数据，则只需要重新处理挖掘结构。 如果将挖掘模型添加到已处理的挖掘结构中，则可以使用 `INSERT INTO MINING MODEL` 语句针对现有数据为新的挖掘模型定型。  
  
 由于市场篮挖掘结构包含嵌套表，因此，需要使用嵌套表结构定义要定型的挖掘列，并使用 `SHAPE` 命令定义从源表请求定型数据的查询。  
  
## <a name="insert-into-statement"></a>INSERT INTO 语句  
 为了定型市场篮挖掘结构及其关联的挖掘模型，请使用[INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx)语句。 可以将该语句中的代码分为下列几部分。  
  
-   标识挖掘结构  
  
-   列出挖掘结构中的列  
  
-   使用 `SHAPE` 定义定型数据  
  
 下面是 `INSERT INTO` 语句的一般示例：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],'<nested SELECT statement>')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 代码的第一行标识将定型的挖掘结构：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 代码的接下来各行指定该挖掘结构定义的列。 必须列出挖掘结构的每一列，并且每列必须映射到源查询数据所包含的对应列。 可以使用 `SKIP` 来忽略源数据中存在但挖掘结构中不存在的列。 有关如何使用详细信息`SKIP`，请参阅[插入到&#40;DMX&#41;](/sql/dmx/insert-into-dmx)。  
  
```  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
```  
  
 代码的最后几行定义将用于定型挖掘结构的数据。 由于源数据包含在两个表中，因此，将使用 `SHAPE` 来关联这两个表。  
  
```  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],''<nested SELECT statement>'')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 在本课中，您将使用 `OPENQUERY` 来定义源数据。 有关针对源数据定义查询的其他方法的信息，请参阅[&#60;源数据查询&#62;](/sql/dmx/source-data-query)。  
  
## <a name="lesson-tasks"></a>课程任务  
 在本课程中，将执行以下任务：  
  
-   处理市场篮挖掘结构  
  
## <a name="processing-the-market-basket-mining-structure"></a>处理市场篮挖掘结构  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>使用 INSERT INTO 处理挖掘结构  
  
1.  在中**对象资源管理器**，右键单击该实例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，依次指向**新查询**，然后单击**DMX**。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  将 INSERT INTO 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    [<mining structure>]  
    ```  
  
     使用：  
  
    ```  
    Market Basket  
    ```  
  
4.  将  
  
    ```  
    <mining structure columns>  
    [<nested table>]  
    ( SKIP, <skipped column> )  
    ```  
  
     使用：  
  
    ```  
    [OrderNumber],  
    [Products]   
    (SKIP, [Model])  
    ```  
  
     在语句中，`Products` 指代 SHAPE 语句定义的 Products 表。 `SKIP` 用于忽略 Model 列，该列在源数据中作为键存在，但是挖掘结构未使用它。  
  
5.  将  
  
    ```  
    SHAPE {  
      OPENQUERY([<datasource>],'<SELECT statement>') }  
    APPEND  
    (   
      {OPENQUERY([<datasource>],'<nested SELECT statement>')  
    }  
    RELATE [<case key>] TO [<foreign key>]  
    ) AS [<nested table>]  
    ```  
  
     使用：  
  
    ```  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
     源查询引用[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]数据源中定义[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]示例项目。 它使用此数据源访问 vAssocSeqLineItems 和 vAssocSeqOrders 视图。 这些视图包含将用于定型挖掘模型的源数据。 如果尚未创建此项目或这些视图，请参阅[数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)。  
  
     在 `SHAPE` 命令中，将使用 `OPENQUERY` 定义两个查询。 第一个查询定义父表，第二个查询定义嵌套表。 这两个表是使用 OrderNumber 列关联的，两个表中都包含该列。  
  
     现在，完整的语句应该如下所示：  
  
    ```  
    INSERT INTO MINING STRUCTURE [Market Basket]  
    (  
       [OrderNumber],[Products] (SKIP, [Model])  
    )  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
6.  上**文件**菜单上，单击**另存 dmxquery1.dmx 另存为**。  
  
7.  在中**另存为**对话框中，浏览到相应的文件夹，并将文件命名`Process Market Basket.dmx`。  
  
8.  在工具栏上，单击**Execute**按钮。  
  
 在该查询完成运行之后，可以查看已经找到的模式和项集，查看关联，或按项集、概率或重要性进行筛选。 若要查看此信息在[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，右键单击数据模型的名称，然后单击**浏览**。  
  
 在下一课中，您将基于添加到市场篮结构中的挖掘模型创建多个预测。  
  
## <a name="next-lesson"></a>下一课  
 [第 4 课：执行市场篮预测](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
  
  
