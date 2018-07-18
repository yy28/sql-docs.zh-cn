---
title: Analysis Services 教程补充课程： 不规则层次结构 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bc5a2164576e2e6142d8835dad6f6c114b7a9c5b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38042301"
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>补充课程-不规则层次结构

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本补充课程中，则当包含空白值 （成员） 在不同级别的层次结构进行透视时解决常见的问题。 例如，组织的高级别经理将部门经理和非经理人员作为直接下属。 或者，地理层次结构包含国家/地区-区域-城市，其中某些城市没有父州或省，如华盛顿特区，梵蒂冈城。 当层次结构具有空白成员时，它通常降低到不同，或右边未对齐，级别。

![as-lesson-detail-ragged-hierarchies-table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

在 1400年兼容级别表格模型有一个额外**隐藏成员**层次结构的属性。 **默认**设置假定在任何级别上没有空白成员。 **隐藏空白成员**设置添加到数据透视表或报表时，层次结构中排除空白成员。  
  
学完本课的估计时间： **20 分钟**  
  
## <a name="prerequisites"></a>必要條件  
本文补充课程是表格建模教程的一部分。 执行任务之前在本补充课程中，应当已完成前面的课程或具有已完成的 Adventure Works Internet Sales 示例模型项目。 

如果已创建 AW Internet Sales 项目作为本教程的一部分，您的模型不尚未包含任何数据或不规则的层次结构。 若要完成本补充课程中，首先需要通过添加一些其他表中创建问题、 创建关系、 计算的列、 度量值和新的组织层次结构。 该部分需要花费大约 15 分钟。 然后，您可以解决此问题在几分钟。  

## <a name="add-tables-and-objects"></a>添加表和对象
  
### <a name="to-add-new-tables-to-your-model"></a>若要将新表添加到您的模型
  
1.  在表格模型资源管理器，展开**数据源**，然后右键单击你的连接 >**导入新表**。
  
2.  在导航器中，选择**DimEmployee**并**FactResellerSales**，然后单击**确定**。

3.  在查询编辑器中，单击**导入**

4.  创建以下[关系](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | 表 1           | “列”       | 筛选器方向   | 表 2     | “列”      | 在职 |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | ，则“默认”            | DimDate     | date        | 是    |
    | FactResellerSales | DueDate      | ，则“默认”            | DimDate     | date        | “否”     |
    | FactResellerSales | ShipDateKey  | ，则“默认”            | DimDate     | date        | “否”     |
    | FactResellerSales | ProductKey   | ，则“默认”            | DimProduct  | ProductKey  | 是    |
    | FactResellerSales | EmployeeKey  | 对两个表 | DimEmployee | EmployeeKey | 是    |

5. 在中**DimEmployee**表中，创建以下[计算列](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

    **路径** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **fullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **级别 1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **级别 2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],2,1)) 
    ```

    **级别 3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],3,1)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],4,1)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],5,1)) 
    ```

6.  在中**DimEmployee**表中，创建[层次结构](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)名为**组织**。 以下列按顺序添加： **Level1**， **Level2**， **Level3**， **Level4**， **Level5**。

7.  在中**FactResellerSales**表中，创建以下[度量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  使用[在 Excel 中的分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)打开 Excel 并自动创建数据透视表。

9.  在中**数据透视表字段**，添加**组织**层次结构从**DimEmployee**表**行**，和**ResellerTotalSales**度量值从**FactResellerSales**表向**值**。

    ![as-lesson-detail-ragged-hierarchies-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    您可以看到该数据透视表中，该层次结构显示了不规则的行。 有很多行显示了空白成员。

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>若要通过设置属性的隐藏成员来修复不规则层次结构

1.  在中**表格模型资源管理器**，展开**表** > **DimEmployee** > **层次结构** > **组织**。

2.  在中**属性** > **隐藏成员**，选择**隐藏空白成员**。 

    ![as-lesson-detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  回到 Excel 中，刷新数据透视表。 

    ![as-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    现在看起来好多 ！

## <a name="see-also"></a>请参阅   
[第 9 课：创建层次结构](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[补充课程-动态安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[补充课程-详细信息行](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
