---
title: 使用多维数据集写回 (MDX) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dc950c69a25ff976b8cdf1cd7cb4252c2584e0af
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-data-modification---using-cube-writebacks"></a>MDX 数据修改的使用多维数据集写回
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  可以使用 [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) 语句更新多维数据集。 通过此语句，您可以使用特定值更新元组。 若要有效地使用 UPDATE CUBE 语句更新多维数据集，必须了解该语句的语法、发生错误的条件以及更新可能对多维数据集产生的影响。  
  
## <a name="update-cube-statement-syntax"></a>UPDATE CUBE 语句的语法  
 下列语法描述了 UPDATE CUBE 语句：  
  
```  
UPDATE [CUBE] <Cube_Name> SET <tuple>.VALUE = <value> [,<tuple>.VALUE = <value>...]  
 [ USE_EQUAL_ALLOCATION | USE_EQUAL_INCREMENT |  
  USE_WEIGHTED_ALLOCATION [BY <weight value_expression>] |  
  USE_WEIGHTED_INCREMENT [BY <weight value_expression>] ]   
```  
  
 如果未为元组指定所有坐标，未指定的坐标将使用层次结构的默认成员。 所标识的元组必须引用使用 [Sum](../../../mdx/sum-mdx.md) 函数聚合的单元，并且不能将计算成员作为该单元的一个坐标使用。  
  
 可以将 UPDATE CUBE 语句视为一个子例程，该子例程生成原子单元的一系列单独的写回操作。 然后，所有这些单独的写回操作汇总出一个指定的和。  
  
> [!NOTE]  
>  如果更新的单元不相互重叠，则 **Update Isolation Level** 连接字符串属性可用于提高 UPDATE CUBE 的性能。 有关详细信息，请参阅 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>。  
  
## <a name="example"></a>示例  
 您可以使用 Adventure Works 多维数据集中的 Sales Targets 度量值组来测试 UPDATE CUBE。 此度量值组包含由 SUM 聚合的度量值，这是 UPDATE CUBE 的一个要求。  
  
1.  为 Adventure Works 数据库的 Sales Targets 度量值组启用写回。 在 Management Studio 中，右键单击度量值组，指向“写回选项”，然后选择“启用写回”。  
  
     您应在 Writeback 文件夹中看到一个新的写回表。 该表的名称为 WriteTable_Fact Sales Quota。  
  
2.  打开 MDX 查询窗口。 运行以下 select 语句以查看原始值：  
  
    ```  
    SELECT [Measures].[Sales Amount Quota] on 0 ,  
    [Employee].[Employee Department].[Title].&[Sales Representative].children on 1  
    FROM [Adventure Works]  
  
    ```  
  
     您应看到每个代表的销售配额。  
  
3.  运行 update cube 语句以写回新值。 在此示例中，我们将销售配额设置为 0。 由于新值为 0，请不要指定分配方法。  
  
    ```  
    UPDATE CUBE [Adventure Works]   
    SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 0  
  
    ```  
  
4.  重新运行 SELECT 语句。 您现在应看到配额为零。  
  
 写回值约束为仅用于当前会话。 若要在各用户和会话之间保留该值，请处理写回表。 在 Management Studio 中，右键单击“WriteTable_Fact Sales Quota”，然后选择“处理”。  
  
 若要指定分配方法，新值必须大于零。 在此示例中，“Sales Amount Quota”的新值为两百万，该分配方法将该金额在所有销售代表之间进行分配。  
  
```  
UPDATE CUBE [Adventure Works]   
SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 2000000   
USE_EQUAL_ALLOCATION  
```  
  
## <a name="error-conditions"></a>错误条件  
 下表介绍了可能导致写回失败的原因以及这些错误的结果。  
  
|错误条件|结果|  
|---------------------|------------|  
|更新包括同一维度中不能共存的成员。|更新将失败。 多维数据集空间将不包含被引用单元。|  
|更新包括作为无符号类型的度量值的来源的度量值。|更新将失败。 增量需要度量值能够取负值。|  
|更新包括执行非求和聚合的度量值。|已引发错误。|  
|尝试更新子多维数据集。|已引发错误。|  
  
## <a name="affect-of-cube-changes"></a>多维数据集更改的影响  
 下列更改将不会对写回产生影响：  
  
-   处理多维数据集、多维数据集的度量值组或多维数据集的维度。  
  
-   向任何维度中添加属性。  
  
-   添加新维度。  
  
-   删除不包含写回的维度。  
  
-   添加、修改或删除层次结构。  
  
-   添加新度量值。  
  
 只有删除写回数据才能进行下列更改：  
  
-   删除属性或其属性层次结构（如果该属性包含在写回中）。 这包括显式删除属性或其属性层次结构，或者删除属性的父维度。  
  
-   删除写回中包含的度量值。  
  
-   向写回中包含的维度添加不带“(全部)”级别的属性。  
  
-   更改写回中包含的维度的维度粒度。  
  
## <a name="see-also"></a>另请参阅  
 [修改数据 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-modifying-data.md)  
  
  
