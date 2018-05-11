---
title: 使用 DRILLTHROUGH 检索源数据 (MDX) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ff067aefccfcf59353236ae9e22c54acb8ebd3b7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-data-manipulation---retrieve-source-data-using-drillthrough"></a>MDX 数据操作-使用 DRILLTHROUGH 检索源数据
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  多维表达式 (MDX) 使用 [DRILLTHROUGH](../../../mdx/mdx-data-manipulation-drillthrough.md)语句从多维数据集单元的源数据中检索行集。  
  
 为了对多维数据集运行 **DRILLTHROUGH** 语句，必须为该多维数据集定义钻取操作。 若要定义钻取操作，请在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]的多维数据集设计器中，在 **“操作”** 窗格的工具栏上单击 **“新建钻取操作”**。 在新的钻取操作中，指定 **DRILLTHROUGH** 语句返回的操作名称、目标、条件以及列。  
  
## <a name="drillthrough-statement-syntax"></a>DRILLTHROUGH 语句的语法  
 **DRILLTHROUGH** 语句使用以下语法：  
  
```  
<drillthrough> ::= DRILLTHROUGH [<Max_Rows>] [<First_Rowset>] <MDX select> [<Return_Columns>]  
   < Max_Rows> ::= MAXROWS <positive number>  
   <First_Rowset> ::= FIRSTROWSET <positive number>  
   <Return_Columns> ::= RETURN <member or attribute> [, <member or attribute>]  
```  
  
 **SELECT** 子句标识包含要检索的源数据的多维数据集单元。 此 **SELECT** 子句与普通 MDX **SELECT** 语句基本相同，不同之处在于在 **SELECT** 子句中，只能在每个轴上指定一个成员。 如果在一个轴上指定了多个成员，则会发生错误。  
  
 `<Max_Rows>` 语法指定返回的每个行集中的最大行数。 如果用于连接数据源的 OLE DB 提供程序不支持 **DBPROP_MAXROWS**， `<Max_Rows>` 设置将被忽略。  
  
 `<First_Rowset>` 语法标识最先返回其行集的分区。  
  
 `<Return_Columns>` 语法标识要返回的基础数据库列。  
  
## <a name="drillthrough-statement-example"></a>DRILLTHROUGH 语句的示例  
 下面的示例说明了 **DRILLTHROUGH** 语句的使用。 在此示例中，DRILLTHROUGH 语句沿着 Stores 维度（切片器轴）查询 Store 维度、Product 维度和 Time 维度的叶，然后返回部门度量值组、部门 ID 和员工的名字。  
  
```  
DRILLTHROUGH  
Select {Leaves(Store), Leaves(Product), Leaves(Time),*} on 0  
From Stores  
RETURN [Department MeasureGroup].[Department Id], [Employee].[First Name]  
```  
  
## <a name="see-also"></a>另请参阅  
 [操作数据 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
