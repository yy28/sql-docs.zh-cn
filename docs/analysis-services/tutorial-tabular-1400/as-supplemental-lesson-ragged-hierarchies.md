---
title: Analysis Services 教程补充课程： 不规则层次结构 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e38e1e2b888ce92fad826fda43624e19a75c2110
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>补充课程-不规则层次结构

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在此补充课程中，则当包含空白值 （成员） 在不同级别的层次结构上进行透视时解决常见的问题。 例如，组织其中高层管理人员都具有部门经理和直接下属作为非经理。 或者，地理层次结构组成的国家/地区-区域的城市，其中某些城市缺少父州或省，如华盛顿特区。，梵蒂冈城。 当层次结构具有空成员时，它通常会降至不同的或右边未对齐，级别。

![as-lesson-detail-ragged-hierarchies-table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

在 1400年兼容性级别的表格模型还有附加**隐藏成员**层次结构的属性。 **默认**设置假设在任何级别没有空白的成员。 **隐藏空成员**设置从层次结构添加到数据透视表或报表时不包括空成员。  
  
学完本课的估计时间： **20 分钟**  
  
## <a name="prerequisites"></a>必要條件  
补充课程本文是表格建模教程的一部分。 之前在本课程中补充执行任务，你应完成前面的课程中所有或具有已完成的 Adventure Works Internet Sales 示例模型项目。 

如果你已创建 AW Internet Sales 项目作为本教程的一部分，您的模型尚不包含任何数据或右边未对齐的层次结构。 若要完成本补充课程中，首先需要通过添加一些其他的表创建问题、 创建关系、 计算的列、 度量值和新的组织层次结构。 该部分需要大约 15 分钟。 然后，您可以在几分钟内解决它。  

## <a name="add-tables-and-objects"></a>添加表和对象
  
### <a name="to-add-new-tables-to-your-model"></a>若要将新表添加到你的模型
  
1.  在表格模型资源管理器，展开**数据源**，然后右键单击你的连接 >**导入新表**。
  
2.  在导航器中，选择**DimEmployee**和**FactResellerSales**，然后单击**确定**。

3.  在查询编辑器中，单击**导入**

4.  创建以下[关系](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | 表 1           | 列       | 筛选器方向   | 表 2     | 列      | 在职 |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | 默认            | DimDate     | 日期        | 是    |
    | FactResellerSales | DueDate      | 默认            | DimDate     | 日期        | 否     |
    | FactResellerSales | ShipDateKey  | 默认            | DimDate     | 日期        | 否     |
    | FactResellerSales | ProductKey   | 默认            | DimProduct  | ProductKey  | 是    |
    | FactResellerSales | EmployeeKey  | 两个表 | DimEmployee | EmployeeKey | 是    |

5. 在**DimEmployee**表中，创建以下[计算列](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

    **路径** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
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

6.  在**DimEmployee**表中，创建[层次结构](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)名为**组织**。 添加以下列中的顺序： **Level1**， **Level2**， **Level3**， **Level4**， **Level5**。

7.  在**FactResellerSales**表中，创建以下[度量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  使用[在 Excel 中的分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)打开 Excel 并自动创建数据透视表。

9.  在**数据透视表字段**，添加**组织**层次结构免遭**DimEmployee**表**行**，和**ResellerTotalSales**度量值，从**FactResellerSales**表**值**。

    ![as-lesson-detail-ragged-hierarchies-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    正如您可以看到数据透视表中，层次结构显示右边未对齐的行。 有许多空白成员其中会显示的行。

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>若要通过将属性设置的隐藏成员修复不规则层次结构

1.  在**表格模型资源管理器**，展开**表** > **DimEmployee** > **层次结构** > **组织**。

2.  在**属性** > **隐藏成员**，选择**隐藏空成员**。 

    ![as-lesson-detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  返回在 Excel 中，刷新数据透视表。 

    ![as-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    现在，这看起来好整个得多 ！

## <a name="see-also"></a>另请参阅   
[Lesson 9： 创建层次结构](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[补充课程-动态安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[补充课程-详细信息行](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
