---
title: 第2课：向市场篮挖掘结构中添加挖掘模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d96a7a7d-35d7-4b34-abb5-f0822c256253
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b9573d9359983e33cf23533787c26039572710ea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63204718"
---
# <a name="lesson-2-adding-mining-models-to-the-market-basket-mining-structure"></a>第 2 课：向市场篮挖掘结构中添加挖掘模型
  在本课中，您将向在[第1课：创建市场篮挖掘结构](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)中创建的市场篮挖掘结构中添加两个挖掘模型。 您可以通过这些挖掘模型创建预测。  
  
 若要预测客户往往同时购买的产品类型，您将使用[Microsoft 关联算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)创建两个挖掘模型，并为*MINIMUM_PROBABILTY*参数创建两个不同的值。  
  
 *MINIMUM_PROBABILTY*是一[!INCLUDE[msCoName](../includes/msconame-md.md)]种关联算法参数，通过指定规则必须具有的最小概率，有助于确定挖掘模型将包含的规则数。 例如，如果此值设置为 0.4，则表明仅当规则所描述的产品组合具有至少 40% 的发生概率时才可生成此规则。  
  
 您将在后面的课程中查看更改*MINIMUM_PROBABILTY*参数的效果。  
  
## <a name="alter-mining-structure-statement"></a>ALTER MINING STRUCTURE 语句  
 若要将包含嵌套表的挖掘模型添加到挖掘结构，请使用[&#40;DMX&#41;语句的 ALTER 挖掘 structure](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016) 。 可以将语句中的代码分为下列几部分：  
  
-   标识挖掘结构  
  
-   命名挖掘模型  
  
-   定义键列  
  
-   定义输入列和可预测列  
  
-   定义嵌套表列  
  
-   标识算法和参数更改  
  
 下面是 `ALTER MINING STRUCTURE` 语句的一般示例，它将包含嵌套表列的挖掘模型添加到结构中：  
  
```  
ALTER MINING STRUCTURE [<Mining Structure Name>]  
ADD MINING MODEL [<Mining Model Name>]  
(  
    [<key column>],  
    <mining model column> <usage>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
) USING <algorithm>( <algorithm parameters> )  
```  
  
 上述代码的第一行标识要向其添加挖掘模型的现有挖掘结构：  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 代码的第二行对将要添加到挖掘结构中的挖掘模型进行命名：  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 有关在数据挖掘扩展插件（DMX）中命名对象的信息，请参阅[标识符 &#40;DMX&#41;](/sql/dmx/identifiers-dmx)。  
  
 代码的接下来的各行对挖掘结构中将由挖掘模型使用的各列进行定义：  
  
```  
[<key column>],  
<mining model columns> <usage>,  
```  
  
 您可以只使用挖掘结构中已有的列。  
  
 挖掘模型列的列表中的第一列必须为挖掘结构中的键列。 但是，您不必在键列的`KEY`后面键入来指定用法。 这是因为您在创建挖掘结构时已将列定义为键。  
  
 其他行指定新挖掘模型中的列的用法。 您可以使用以下语法指定挖掘模型中的列将用于预测：  
  
```  
<column name> PREDICT,  
```  
  
 如果没有指定用法，则不必在列表中包含数据挖掘结构列。 由引用的数据挖掘结构所使用的所有列可自动用于基于该结构的挖掘模型中。 但是，除非您指定用法，否则模型不会将这些列用于定型。  
  
 代码的最后一行定义将用于生成挖掘模型的算法和算法参数。  
  
```  
) USING <algorithm>( <algorithm parameters> )  
```  
  
## <a name="lesson-tasks"></a>课程任务  
 您将在本课中执行以下任务：  
  
-   使用默认的概率向结构中添加关联挖掘模型  
  
-   使用修改的概率向结构中添加关联挖掘模型  
  
## <a name="adding-an-association-mining-model-to-the-structure-using-the-default-minimum_probability"></a>使用默认的 MINIMUM_PROBABILITY 向结构中添加关联挖掘模型  
 第一个任务是使用*MINIMUM_PROBABILITY*的默认值将新的挖掘模型添加到市场篮挖掘[!INCLUDE[msCoName](../includes/msconame-md.md)]结构中。  
  
#### <a name="to-add-an-association-mining-model"></a>添加关联挖掘模型  
  
1.  在**对象资源管理器**中，右键单击实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向 "**新建查询**"，然后单击 " **DMX**"。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
    > [!NOTE]  
    >  若要对特定的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库创建 DMX 查询，请右键单击该数据库而不是右键单击实例。  
  
2.  将 `ALTER MINING STRUCTURE` 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    <mining structure name>   
    ```  
  
     替换为：  
  
    ```  
    [Market Basket]  
    ```  
  
4.  将  
  
    ```  
    <mining model name>   
    ```  
  
     替换为：  
  
    ```  
    [Default Association]  
    ```  
  
5.  将  
  
    ```  
    [<key column>],  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     替换为：  
  
    ```  
    OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     在本例中，`[Products]` 表已被指定为可预测列`.`。此外，`[Model]` 列包含于嵌套表列的列表中，原因是它是嵌套表的键列。  
  
    > [!NOTE]  
    >  请注意，嵌套键不同于事例键。 事例键是事例的唯一标识符，而嵌套键是您想要建模的属性。  
  
6.  将  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     替换为：  
  
    ```  
    Using Microsoft_Association_Rules  
    ```  
  
     现在，结果语句应该如下所示：  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Default Association]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    Using Microsoft_Association_Rules  
    ```  
  
7.  在 "**文件**" 菜单上，单击 "**将 DMXQuery1 另存为**"。  
  
8.  在 "**另存为**" 对话框中，浏览到相应的文件夹，并将`Default_Association_Model.dmx`该文件命名为。  
  
9. 在工具栏上，单击 "**执行**" 按钮。  
  
## <a name="adding-an-association-mining-model-to-the-structure-changing-the-default-minimum_probability"></a>向结构中添加关联挖掘模型并更改默认的 MINIMUM_PROBABILITY  
 下一个任务是根据 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联算法，向市场篮挖掘结构中添加新的挖掘模型，并将 MINIMUM_PROBABILITY 的默认值改为 0.01。 更改参数会导致 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联算法创建更多的规则。  
  
#### <a name="to-add-an-association-mining-model"></a>添加关联挖掘模型  
  
1.  在**对象资源管理器**中，右键单击实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向 "**新建查询**"，然后单击 " **DMX**"。  
  
     将打开查询编辑器，其中包含一个新的空白查询。  
  
2.  将 `ALTER MINING STRUCTURE` 语句的一般示例复制到空白查询中。  
  
3.  将  
  
    ```  
    <mining structure name>   
    ```  
  
     替换为：  
  
    ```  
    Market Basket  
    ```  
  
4.  将  
  
    ```  
    <mining model name>   
    ```  
  
     替换为：  
  
    ```  
    [Modified Association]  
    ```  
  
5.  将  
  
    ```  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     替换为：  
  
    ```  
    OrderNumber,  
    [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     在本例中，`[Products]` 表已被指定为可预测列。 此外，`[MODEL]` 列包含于列表中，原因在于它是嵌套表的键列。  
  
6.  将  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     替换为：  
  
    ```  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
     现在，结果语句应该如下所示：  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Modified Assocation]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
7.  在 "**文件**" 菜单上，单击 "**将 DMXQuery1 另存为**"。  
  
8.  在 "**另存为**" 对话框中，浏览到相应的文件夹，并将`Modified Association_Model.dmx`该文件命名为。  
  
9. 在工具栏上，单击 "**执行**" 按钮。  
  
 在下一课中，您将处理市场篮挖掘结构及其关联的挖掘模型。  
  
## <a name="next-lesson"></a>下一课  
 [第 3 课：处理市场篮挖掘结构](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
  
  
