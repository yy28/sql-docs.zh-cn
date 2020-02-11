---
title: 选择 " &lt;源&gt;结构"。事例 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 041d6ade2363b4a33528bd44438a2fcb440d61ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928297"
---
# <a name="select-from-ltstructuregtcases"></a>选择 " &lt;源&gt;结构"。这
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回用于创建挖掘结构的事例。  
  
 如果未对结构启用钻取功能，则该语句将失败。 此外，如果用户在挖掘结构上没有钻取权限，则该语句也会失败。  
  
 在[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中，默认情况下将启用对新挖掘结构的钻取功能。 若要验证是否为特定结构启用了钻取，请检查**CacheMode**属性的值是否设置为**KeepTrainingCases**。  
  
 如果**CacheMode**的值更改为**ClearAfterProcessing**，则将从缓存中清除结构事例，并且不能使用钻取。  
  
> [!NOTE]  
>  不能使用数据挖掘扩展插件 (DMX) 在挖掘结构上启用或禁用钻取功能。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT [TOP n] <expression list> FROM <structure>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>参数  
 *n*  
 可选。 一个指定返回行数的整数。  
  
 *表达式列表*  
 一个逗号分隔的表达式列表。  
  
 该表达式可以包括列标识符、用户定义函数和 VBA 函数。  
  
 *构造*  
 结构的名称。  
  
 *条件表达式*  
 一个限制条件，用于限制从列列表返回的值。  
  
 *表达式*  
 可选。 一个返回标量值的表达式。  
  
## <a name="remarks"></a>备注  
 如果对模型和结构都启用了钻取功能，则拥有挖掘结构和模型钻取权限的角色的任何成员都可以使用下面的语法返回模型中未包括的结构列。  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 因此，为了保护敏感数据或个人信息，应构造数据源视图来屏蔽个人信息，并且仅在需要时才授予对挖掘结构或挖掘模型的**AllowDrillthrough**权限。  
  
## <a name="examples"></a>示例  
 下面的示例基于挖掘结构，目标邮件基于[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]数据库和关联的挖掘模型。 有关详细信息，请参阅[数据挖掘基础教程](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。  
  
### <a name="example-1-drill-through-to-structure-cases"></a>示例 1：钻取到结构事例  
 下面的示例返回挖掘结构“目标邮件”中 500 名年龄最大的客户的列表。 查询返回挖掘模型中的所有列，但将行限制为购买过自行车的客户，并且按年龄进行排序。 您还可以编辑表达式列表以便仅返回需要的列。  
  
```  
SELECT TOP 500 *  
FROM [Targeted Mailing].Cases  
WHERE [Bike Buyer] = 1  
ORDER BY Age DESC;  
```  
  
### <a name="example-2-drillthrough-to-test-or-training-cases-only"></a>示例 2：只钻取到测试或定型事例  
 下面的示例返回保留用于测试的目标邮件的结构事例列表。 如果挖掘结构不包含维持测试集，则默认将所有事例视为定型事例，并且此查询返回 0 个事例。  
  
```  
SELECT [Customer Key], Gender, Age  
FROM [Targeted Mailing].Cases  
WHERE IsTestCase();  
```  
  
 若要返回定型事例，请替换函数 `IsTrainingCase()`。  
  
## <a name="see-also"></a>另请参阅  
 [选择 &#40;DMX&#41;](../dmx/select-dmx.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
