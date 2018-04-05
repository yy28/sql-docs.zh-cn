---
title: 将插入 (DMX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- INSERT INTO
- INSERT
- INSERT_INTO
dev_langs:
- DMX
helpviewer_keywords:
- SKIP (DMX)
- mapped model columns element
- source data query element
- <mapped model columns> element
- <source data query> element
- INSERT INTO statement
- mining models [Analysis Services], processing
- training mining models
- mining structures [DMX], processing
ms.assetid: 85eed207-396c-4a95-a74e-2acc1abc7e2c
caps.latest.revision: 49
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 70b2acdd5370be93f4fca9a5270a5b9951305248
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  处理指定的数据挖掘对象。 有关处理挖掘模型和挖掘结构的详细信息，请参阅[处理要求和注意事项 &#40; 数据挖掘 &#41;](../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 如果指定了挖掘结构，则该语句将处理挖掘结构及其关联的所有挖掘模型。 如果指定了挖掘模型，则该语句将只处理挖掘模型。  
  
## <a name="syntax"></a>语法  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>参数  
 *model*  
 一个模型标识符。  
  
 *结构*  
 结构标识符。  
  
 *映射的模型列*  
 一组以逗号分隔的列标识符和嵌套标识符。  
  
 *源数据查询*  
 采用提供程序所定义格式的源查询。  
  
## <a name="remarks"></a>Remarks  
 如果不指定**挖掘模型**或**挖掘结构**，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]搜索依据的名称，该对象类型并处理正确的对象。 如果服务器包含同名的挖掘结构和挖掘模型，将返回错误。  
  
 通过使用第二种语法形式，INSERT INTO*\<对象 >*。COLUMN_VALUES，你可以将数据直接插入模型列而无需训练模型。 该方法以一种简练、有序的方式向模型提供列数据，在处理包含层次结构或有序列的数据集时，该方法很有用。  
  
 如果你使用**INSERT INTO**与挖掘模型或挖掘结构和关闭的离开\<映射模型列 > 和\<源数据查询 > 自变量，该语句的行为类似**ProcessDefault**，使用已存在的绑定。 如果绑定不存在，则语句将返回错误。 有关详细信息**ProcessDefault**，请参阅[处理选项和设置 &#40;Analysis Services &#41;](../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md). 下例说明了该语法：  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 如果指定**挖掘模型**并提供处理映射的列、 源数据查询、 模型和相关联的结构。  
  
 下表说明了不同形式的语句在不同对象状态下返回的结果。  
  
|。|对象状态|结果|  
|---------------|----------------------|------------|  
|插入到挖掘模型*\<模型 >*|处理挖掘结构。|处理挖掘模型。|  
||未处理挖掘结构。|处理挖掘模型和挖掘结构。|  
||挖掘结构包含其他挖掘模型。|进程失败。 必须重新处理结构和关联的挖掘模型。|  
|INSERT INTO 挖掘结构*\<结构 >*|处理或未处理挖掘结构。|处理挖掘结构和关联的挖掘模型。|  
|插入到挖掘模型*\<模型 >* ，它包含源查询<br /><br /> 或多个<br /><br /> INSERT INTO 挖掘结构*\<结构 >* ，它包含源查询|结构或模型已包含内容。|进程失败。 通过执行此操作之前，必须清除的对象[删除 &#40; DMX &#41;](../dmx/delete-dmx.md)。|  
  
## <a name="mapped-model-columns"></a>映射的模型列  
 通过使用\<映射模型列 > 元素，可以在挖掘模型映射到的列中的数据源的列。 \<映射模型列 > 元素具有以下形式：  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 通过使用**跳过**，你可以排除某些列，必须存在于源查询，但挖掘模型中不存在。 如果您无法控制输入行集包含的列，则 SKIP 非常有用。 如果您正在编写您自己的 OPENQUERY，更好的做法是从 SELECT 列列表中省略该列，而不是使用 SKIP。  
  
 当需要输入行集中的列来执行联接但该列并非由挖掘结构使用时，SKIP 也将非常有用。 其典型示例是包含嵌套表的挖掘结构和挖掘模型。 此结构的输入行集将包含一个外键列，该外键列用于借助 SHAPE 子句创建分层行集，但在模型中几乎总是不使用该外键列。  
  
 SKIP 语法要求在没有相应挖掘结构列的输入行集的各个列位置中插入 SKIP。 例如，在下面的嵌套表示例中，必须在 APPEND 子句中选择 OrderNumber，以便在 RELATE 子句中使用 OrderNumber 指定联接；但是，您并不希望将 OrderNumber 数据插入到挖掘结构的嵌套表中。 因此，本示例在 INSERT INTO 参数中使用 SKIP 关键字而不是 OrderNumber。  
  
## <a name="source-data-query"></a>源数据查询  
 \<源数据查询 > 元素可以包含以下数据源类型：  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **形状**  
  
-   返回行集的任意 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 查询  
  
 有关数据源类型的详细信息，请参阅[&#60; 源数据查询 &#62;](../dmx/source-data-query.md)。  
  
## <a name="basic-example"></a>基本示例  
 下面的示例使用**OPENQUERY**定型 Naive Bayes 模型中的目标邮递数据基于[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]数据库。  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>嵌套表示例  
 下面的示例使用**形状**训练关联挖掘模型包含嵌套的表。 请注意，第一行包含**跳过**改为 OrderNumber，它在必需**SHAPE_APPEND**语句但不是在挖掘模型中使用。  
  
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
 [数据挖掘扩展插件 &#40; DMX &#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
