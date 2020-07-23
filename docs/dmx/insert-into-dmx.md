---
title: INSERT INTO （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eedff3b14960fae68ad4e3a9ac54a0034c1a9300
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969769"
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  处理指定的数据挖掘对象。 有关处理挖掘模型和挖掘结构的详细信息，请参阅[处理数据挖掘&#41;&#40;要求和注意事项](https://docs.microsoft.com/analysis-services/data-mining/processing-requirements-and-considerations-data-mining)。  
  
 如果指定了挖掘结构，则该语句将处理挖掘结构及其关联的所有挖掘模型。 如果指定了挖掘模型，则该语句将只处理挖掘模型。  
  
## <a name="syntax"></a>语法  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>参数  
 *model*  
 模型标识符。  
  
 *构造*  
 结构标识符。  
  
 *映射的模型列*  
 一组以逗号分隔的列标识符和嵌套标识符。  
  
 *源数据查询*  
 采用提供程序所定义格式的源查询。  
  
## <a name="remarks"></a>备注  
 如果未指定**挖掘模型**或**挖掘结构**，将根据 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 名称搜索对象类型，并处理正确的对象。 如果服务器包含同名的挖掘结构和挖掘模型，将返回错误。  
  
 通过使用第二种语法形式，将插入到 *\<object>* 。COLUMN_VALUES，可以将数据直接插入模型列中，而无需定型模型。 该方法以一种简练、有序的方式向模型提供列数据，在处理包含层次结构或有序列的数据集时，该方法很有用。  
  
 如果对挖掘模型或挖掘结构使用**INSERT INTO** ，并保留 \<mapped model columns> 和 \<source data query> 自变量，则该语句的行为类似于**ProcessDefault**，并使用已经存在的绑定。 如果绑定不存在，则语句将返回错误。 有关**ProcessDefault**的详细信息，请参阅[Analysis Services&#41;&#40;处理选项和设置](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services)。 下例说明了该语法：  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 如果指定**挖掘模型**并提供映射列和源数据查询，则会处理模型和关联的结构。  
  
 下表说明了不同形式的语句在不同对象状态下返回的结果。  
  
|语句|对象状态|结果|  
|---------------|----------------------|------------|  
|插入挖掘模型*\<model>*|处理挖掘结构。|处理挖掘模型。|  
||未处理挖掘结构。|处理挖掘模型和挖掘结构。|  
||挖掘结构包含其他挖掘模型。|进程失败。 必须重新处理结构和关联的挖掘模型。|  
|插入挖掘结构*\<structure>*|处理或未处理挖掘结构。|处理挖掘结构和关联的挖掘模型。|  
|插入 *\<model>* 包含源查询的挖掘模型<br /><br /> 或<br /><br /> 插入 *\<structure>* 包含源查询的挖掘结构中|结构或模型已包含内容。|进程失败。 在执行此操作之前，必须通过使用[DELETE &#40;DMX&#41;](../dmx/delete-dmx.md)来清除这些对象。|  
  
## <a name="mapped-model-columns"></a>映射的模型列  
 通过使用 \<mapped model columns> 元素，您可以将数据源中的列映射到挖掘模型中的列。 \<mapped model columns>元素具有以下格式：  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 通过使用**SKIP**，可以排除源查询中必须存在但在挖掘模型中不存在的某些列。 如果您无法控制输入行集包含的列，则 SKIP 非常有用。 如果您正在编写您自己的 OPENQUERY，更好的做法是从 SELECT 列列表中省略该列，而不是使用 SKIP。  
  
 当需要输入行集中的列来执行联接但该列并非由挖掘结构使用时，SKIP 也将非常有用。 其典型示例是包含嵌套表的挖掘结构和挖掘模型。 此结构的输入行集将包含一个外键列，该外键列用于借助 SHAPE 子句创建分层行集，但在模型中几乎总是不使用该外键列。  
  
 SKIP 语法要求在没有相应挖掘结构列的输入行集的各个列位置中插入 SKIP。 例如，在下面的嵌套表示例中，必须在 APPEND 子句中选择 OrderNumber，以便在 RELATE 子句中使用 OrderNumber 指定联接；但是，您并不希望将 OrderNumber 数据插入到挖掘结构的嵌套表中。 因此，本示例在 INSERT INTO 参数中使用 SKIP 关键字而不是 OrderNumber。  
  
## <a name="source-data-query"></a>源数据查询  
 \<source data query>元素可以包含以下数据源类型：  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **整形**  
  
-   返回行集的任意 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 查询  
  
 有关数据源类型的详细信息，请参阅[&#60;源数据查询&#62;](../dmx/source-data-query.md)。  
  
## <a name="basic-example"></a>基本示例  
 下面的示例使用**OPENQUERY**基于数据库中的目标邮件数据来训练 Naive Bayes 模型 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 。  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>嵌套表示例  
 下面的示例使用**SHAPE**为包含嵌套表的关联挖掘模型定型。 请注意，前行包含**SKIP** OrderNumber，这在**SHAPE_APPEND**语句中是必需的，但不在挖掘模型中使用。  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
