---
title: "模型筛选器语法和示例（Analysis Services – 数据挖掘） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "模型筛选器 [数据挖掘]"
  - "筛选器语法 [数据挖掘]"
  - "筛选器 [数据挖掘]"
  - "筛选器 [Analysis Services]"
ms.assetid: c729d9b3-8fda-405e-9497-52b2d7493eae
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 17
---
# 模型筛选器语法和示例（Analysis Services – 数据挖掘）
  本节提供有关模型筛选器语法的详细信息以及示例表达式。  
  
 [筛选器语法](#bkmk_syntax)  
  
 [事例属性的筛选器](#bkmk_Ex1)  
  
 [嵌套表属性的筛选器](#bkmk_Ex2)  
  
 [多个嵌套表属性的筛选器](#bkmk_Ex3)  
  
 [嵌套表中缺失的属性的筛选器](#bkmk_Ex4)  
  
 [多个嵌套表值的筛选器](#bkmk_Ex5)  
  
 [嵌套表属性和 EXISTS 的筛选器](#bkmk_Ex6)  
  
 [筛选器组合](#bkmk_Ex7)  
  
 [日期筛选器](#bkmk_Ex8)  
  
##  <a name="bkmk_Syntax"></a> 筛选器语法  
 筛选表达式通常等同于 WHERE 子句的内容。 您可以使用逻辑运算符 **AND**、 **OR**和 **NOT**连接多个条件。  
  
 在嵌套表中，您还可以使用 **EXISTS** 和 **NOT EXISTS** 运算符。 如果子查询至少返回一行，则 **EXISTS** 条件的计算结果为 **true** 。 当您要将模型限制为包含嵌套表中的特殊值的事例时，这将非常有用。例如，客户至少购买过一次某种物品。  
  
 如果在子查询中指定的 **NOT EXISTS** 条件不存在，则该条件的计算结果为 **true** 。 其中一个例子就是您要将模型限制为从未购买过某种特殊物品的客户。  
  
 常规语法如下所示：  
  
```  
<filter>::=<predicate list>  | ( <predicate list> )  
<predicate list>::= <predicate> | [<logical_operator> <predicate list>]   
<logical_operator::= AND| OR  
<predicate>::= NOT <predicate>|( <predicate> ) <avPredicate> | <nestedTablePredicate> | ( <predicate> )   
<avPredicate>::= <columnName> <operator> <scalar> | <columnName> IS [NOT] NULL  
<operator>::= = | != | <> | > | >= | < | <=  
<nestedTablePredicate>::= EXISTS (<subquery>)  
<subquery>::=SELECT * FROM <columnName>[ WHERE  <predicate list> ]  
```  
  
 *filter*  
 包含由逻辑运算符连接的一个或多个谓词。  
  
 *谓词列表*  
 用逻辑运算符分隔的一个或多个有效的筛选表达式。  
  
 *columnName*  
 挖掘结构列的名称。  
  
 逻辑运算符  
 **AND**、**OR**、**NOT**  
  
 *avPredicate*  
 只能应用到标量挖掘结构列的筛选表达式。 *avPredicate* 表达式既可用于模型筛选器中，也可用于嵌套表筛选器中。  
  
 使用以下任何运算符的表达式只能应用到连续列中。 设置用户帐户 ：  
  
-   **\<**（小于）  
  
-   **>**（大于）  
  
-   **>=**（大于或等于）  
  
-   **\<=**（小于或等于）  
  
> [!NOTE]  
>  无论是什么数据类型，这些运算符都不能应用到类型为 **Discrete**、**Discretized** 或 **Key** 的列。  
  
 使用以下任何运算符的表达式可以应用到连续、离散、离散化或键列中：  
  
-   **=**（等于）  
  
-   **!=**（不等于）  
  
-   **为 NULL**  
  
 如果 *avPredicate*参数应用到离散化列中，则筛选器中所用的值可以是特定的存储桶中的任何值。  
  
 换句话说，你没有将条件定义为 `AgeDisc = ’25-35’`，而是计算并使用该区间的值。  
  
 例如，`AgeDisc = 27` 表示与 27 位于同一区间的任何值，在本例中为 25-35。  
  
 *nestedTablePredicate*  
 应用到嵌套表中的筛选表达式。 只能用于模型筛选器中。  
  
 参数的子查询参数 *nestedTablePredicate* 能应用到表挖掘结构列中  
  
 子查询  
 后面跟随有效的谓词或谓词列表的 SELECT 语句。  
  
 所有谓词必须为 *avPredicates*中描述的类型。 而且，谓词只能是由 *columnName*参数标识的当前嵌套表中包含的列。  
  
### 筛选器语法限制  
 下面的限制适用于筛选器：  
  
-   筛选器只能包含简单的谓词。 其中包括数学运算符、标量和列名称。  
  
-   筛选器语法中不支持用户定义函数。  
  
-   筛选器语法中不支持非布尔运算符，如加号或减号。  
  
## 筛选器示例  
 下面的示例演示应用到挖掘模型中的筛选器的用法。 如果使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在筛选器对话框的 **“属性”** 窗口和 **“表达式”** 窗格创建筛选表达式，您将只能看到显示在 WITH FILTER 关键字之后的字符串。 此处包括挖掘结构的定义，从而更易于理解列类型和用法。  
  
###  <a name="bkmk_Ex1"></a> 示例 1：典型的事例级筛选  
 以下示例显示一个简单的筛选器，它将模型中使用的事例限制为其职业为建筑师并且年龄在 30 岁以上的客户。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_1  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH FILTER (Age > 30 AND Occupation=’Architect’)  
```  
  
 [返回页首](#bkmk_Syntax)  
  
###  <a name="bkmk_Ex2"></a> 示例 2：使用嵌套表属性的事例级筛选  
 如果您的挖掘结构包含嵌套表，则您可以对嵌套表中某个值的存在性进行筛选，还可以对包含特定值的嵌套表行进行筛选。 下面的示例将模型所用的事例限制为年龄在 30 岁以上并且至少购买过一次包含牛奶在内的产品的客户。  
  
 如下面的示例所示，不要求筛选器仅使用模型中包含的列。 嵌套表 **产品** 是挖掘结构的一部分，但没有包含在挖掘模型内。 但是，您仍然可以对嵌套表中的值和属性进行筛选。 若要查看这些事例的详细信息，必须启用钻取功能。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_2  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH DRILLTHROUGH,   
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’)  
)  
```  
  
 [返回页首](#bkmk_Syntax)  
  
###  <a name="bkmk_Ex3"></a> 示例 3：对多个嵌套表属性的事例级筛选  
 下面的示例显示一个由三个条件构成的筛选器：第一个条件应用到事例表，第二个条件应用到嵌套表中的一个属性，第三个条件应用到嵌套表列中某一列的特定值。  
  
 筛选器中的第一个条件 `Age > 30`应用到事例表中的某一列。 其他条件都应用到嵌套表。  
  
 第二个条件 `EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’`检查嵌套表中是否至少存在一次包含牛奶在内的产品购买活动。 第三个条件 `Quantity>=2`意味着客户在单次交易中至少购买了两单位的牛奶。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_3  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
)  
)  
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’  AND Quantity >= 2)   
)  
```  
  
 [返回页首](#bkmk_Syntax)  
  
###  <a name="bkmk_Ex4"></a> 示例 4：对嵌套表属性缺失的事例级筛选  
 下面的示例显示如何通过对嵌套表中属性的缺失进行筛选将事例限制为没有购买过特定物品的客户。 在下面的示例中，使用年龄在 30 岁以上并且从未购买过牛奶的客户对模型进行定型。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_4  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName  
)  
)  
FILTER (Age > 30 AND NOT EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’) )  
```  
  
 [返回页首](#bkmk_Syntax)  
  
###  <a name="bkmk_Ex5"></a> 示例 5：对多个嵌套表值进行筛选  
 下面的示例的目的旨在显示嵌套表筛选。 嵌套表筛选器是在事例筛选器之后应用的，并且仅用于限制嵌套表行。  
  
 由于没有指定 EXISTS，因此该模型包含多个嵌套表为空的事例。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_5  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName=’Milk’ OR ProductName=’bottled water’)  
)  
WITH DRILLTHROUGH  
```  
  
 [返回页首](#bkmk_Syntax)  
  
###  <a name="bkmk_Ex6"></a> 示例 6：对嵌套表属性和 EXISTS 的筛选  
 在下面的示例中，嵌套表上的筛选器将行限制为包含牛奶或瓶装水的行。 然后，使用 **EXISTS** 语句对模型中的事例进行限制。 这样即可保证嵌套表不为空。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_6  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName=’Milk’ OR ProductName=’bottled water’)  
)  
FILTER (EXISTS (Products))  
```  
  
 [返回页首](#bkmk_Syntax)  
  
###  <a name="bkmk_Ex7"></a> 示例 7：复杂的筛选器组合  
 此模型的应用场景类似于示例 4，但比示例 4 要复杂得多。 嵌套表 **ProductsOnSale** 的筛选器条件 `(OnSale)` 意味着对于 **ProductName** 中列出的产品，**OnSale** 的值必须为 **true**。 此处 **OnSale** 是一个结构列。  
  
 **ProductsNotOnSale** 的筛选器的第二部分具有相同的语法，但是它是针对其 **OnSale** 的值为 **not true**`(!OnSale)` 的产品进行筛选的。  
  
 最后，这些条件将组合在一起，同时另一个限制将添加到事例表中。 结果是可以对年龄在 25 岁以上的所有客户根据在 **ProductsOnSale** 列表中包含的事例预测其在 **ProductsNotOnSale** 列表中的产品的购买情况。  
  
 `ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_7`  
  
 `(`  
  
 `CustomerId,`  
  
 `Age,`  
  
 `Occupation,`  
  
 `MaritalStatus,`  
  
 `ProductsOnSale`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(OnSale),`  
  
 `ProductsNotOnSale PREDICT ONLY`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(!OnSale)`  
  
 `)`  
  
 `WITH DRILLTHROUGH,`  
  
 `FILTER (EXISTS (ProductsOnSale) AND EXISTS(ProductsNotOnSale) AND Age > 25)`  
  
 [返回页首](#bkmk_Syntax)  
  
###  <a name="bkmk_Ex8"></a> 示例 8：对日期进行筛选  
 您可以像对任何其他数据一样，按日期筛选输入列。 在日期/时间类型的列中包含的日期是连续值；因此，您可以通过使用大于号 (>) 或小于号 (<) 之类的运算符指定日期范围。 如果您的数据源不是按连续数据类型表示日期的，而是将日期表示为离散值或文本值，则不能对日期范围进行筛选，而必须指定单独的离散值。  
  
 但是，如果用于筛选器的日期列也是用于模型的键列，则不能对时序模型中的日期列创建筛选器。 其原因在于，在时序模型以及顺序分析和聚类分析模型中，日期列可作为 **KeyTime** 或 **KeySequence**类型处理。  
  
 如果您需要对时序模型中的连续日期进行筛选，则可以在挖掘结构中创建该列的一个副本，然后对这个新列筛选该模型。  
  
 例如，以下表达式表示针对已添加到 Forecasting 模型的 **Continuous** 类型的日期列的筛选器。  
  
 `=[DateCopy] > '12:31:2003:00:00:00'`  
  
> [!NOTE]  
>  请注意，添加到模型的任何附加列都可能会影响结果。 因此，如果您不希望该列用于序列的计算，则应该仅将该列添加到挖掘结构，而不是添加到模型。 您还可以将针对该列的模型标志设置为 **PredictOnly** 或 **Ignore**。 有关详细信息，请参阅[建模标志（数据挖掘）](../../analysis-services/data-mining/modeling-flags-data-mining.md)。  
  
 对于其他模型类型，您可以将日期用作输入条件或筛选条件，将像在任何其他列中一样。 但是，如果您需要使用 **Continuous** 数据类型不支持的特定级别的粒度，则可以通过使用表达式提取要在筛选和分析中使用的单位，在数据源中创建派生值。  
  
> [!WARNING]  
>  指定日期作为筛选条件时，必须使用以下格式，而与当前操作系统的日期格式无关： `mm/dd/yyyy`。 其他任何格式都会导致错误。  
  
 例如，如果要筛选呼叫中心结果以便只显示周末，则可以在数据源视图中创建一个表达式，该表达式提取每个日期的工作日名称，然后将该工作日名称值用作输入或者在筛选中用作离散值。 只需记住的是，重复值可能会影响模型，因此，您应该只使用某一列，而不是日期列加上派生值。  
  
 [返回页首](#bkmk_Syntax)  
  
## 另请参阅  
 [挖掘模型的筛选器（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [测试和验证（数据挖掘）](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  