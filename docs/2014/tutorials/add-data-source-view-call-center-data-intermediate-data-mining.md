---
title: 添加数据源视图为呼叫中心数据 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a448e7e4-dbd1-4d31-90bc-4d4a1c23b352
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f212c6436af0e35c7cfaceadf8c519765d0a07a6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171939"
---
# <a name="adding-a-data-source-view-for-call-center-data-intermediate-data-mining-tutorial"></a>为呼叫中心数据添加数据源视图（数据挖掘中级教程）
  在本任务中，添加一个将用于访问呼叫中心数据的数据源视图。 将使用相同的数据来生成用于探索的初始神经网络模型以及用于提供建议的逻辑回归模型。  
  
 您还将使用数据源视图设计器向一周中某天添加列。 这是因为尽管源数据按日期跟踪呼叫中心数据，您的经验告诉您呼叫量和服务质量存在重复模式，取决于该天是周末还是工作日。  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-add-a-data-source-view"></a>添加数据源视图  
  
1.  在中**解决方案资源管理器**，右键单击**数据源视图**，然后选择**新数据源视图**。  
  
     系统将打开数据源视图向导。  
  
2.  在“欢迎使用数据源视图向导”页中，单击“下一步”。  
  
3.  上**选择数据源**页面上，在**关系数据源**，选择[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]数据源。 如果没有此数据源，请参阅[数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)。 单击“下一步” 。  
  
4.  上**选择表和视图**页上，选择下面的表，然后单击右箭头以将其添加到数据源视图：  
  
    -   **FactCallCenter (dbo)**  
  
    -   **DimDate**  
  
5.  单击“下一步” 。  
  
6.  上**完成向导**页上，默认情况下，数据源视图命名为[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]。 将名称更改为**CallCenter**，然后单击**完成**。  
  
     数据源视图设计器将打开以显示**CallCenter**数据源视图。  
  
7.  在数据源视图窗格中，右键单击并选择**添加/删除表**。 选择的表**DimDate**然后单击**确定**。  
  
     应之间自动添加关系`DateKey`中每个表的列。 将使用此关系获取列**EnglishDayNameOfWeek**，从**DimDate**表并在模型中使用。  
  
8.  在数据源视图设计器中，右键单击表中， **FactCallCenter**，然后选择**新建命名计算**。  
  
     在中**创建命名计算**对话框框中，键入以下值：  
  
    |||  
    |-|-|  
    |**列名**|DayOfWeek|  
    |**Description**|从 DimDate 表获取一周中的某天|  
    |**表达式**|`(SELECT EnglishDayNameOfWeek AS DayOfWeek FROM DimDate where FactCallCenter.DateKey = DimDate.DateKey)`|  
  
     若要验证表达式创建数据需要请右键单击该表**FactCallCenter**，然后选择**浏览数据**。  
  
9. 花点时间查看可用的数据，以便您可以了解在数据挖掘中如何使用它：  
  
|列名|包含|  
|-----------------|--------------|  
|FactCallCenterID|数据导入到数据仓库中时创建的一个任意键。<br /><br /> 此列标识唯一的记录并应作为数据挖掘模型的事例键。|  
|DateKey|呼叫中心运营的日期，以整数表示。 整数日期键在数据仓库中经常用到，但是如果要按日期值分组，您可能要获取日期/时间格式的日期。<br /><br /> 请注意由于供应商为每个运营日中的每个班次都提供了一个单独的报表，因此日期不是唯一的。|  
|WageType|指示当天是工作日、 周末或假期。<br /><br /> 很可能是由于客户服务的质量在工作日与周末因此您将使用此列作为输入。|  
|班次|指示为其记录呼叫的轮班时间。 此呼叫中心将工作日划分为四个轮班时间：AM、PM1、PM2 和 Midnight。<br /><br /> 班次可能影响客户服务质量，因此您将使用此列作为输入。|  
|LevelOneOperators|指示值班的一级接线员的数量。<br /><br /> 呼叫中心的员工最低级别为 l 级，因此这些员工经验不足。|  
|LevelTwoOperators|指示值班的二级接线员的数量。<br /><br /> 员工必须记录一定数量的服务小时数才会被视为第二级操作员。|  
|TotalOperators|此轮班时间内存在的接线员的总数。|  
|Calls|此轮班时间内收到的呼叫数。|  
|AutomaticResponses|完全通过自动呼叫处理（交互式语音应答，即 IVR）来处理的呼叫数。|  
|Orders|由呼叫产生的订单数。|  
|IssuesRaised|由呼叫产生的需要后续操作的问题的数量。|  
|AverageTimePerIssue|应答一次来电所需的平均时间。|  
|ServiceGrade|一个度量值，指示对常规质量的服务，以度量*挂断率*整个班次的。 挂断率越高，说明客户的满意度越差，因此丢失潜在订单的可能性也就越大。|  
  
 请注意，数据包含基于单个日期列的四个不同列： `WageType`， **DayOfWeek**， `Shift`，和`DateKey`。 通常在数据挖掘中不要使用派生自同一数据的多个列，因为值之间的相关性太强，可能遮盖其他模式。  
  
 但是，我们将不会使用`DateKey`模型中因为它包含唯一值太多。 之间没有直接关系`Shift`并**DayOfWeek**，和`WageType`并**DayOfWeek**只部分相关。 如果您担心共线性，可以使用所有可用列创建结构，然后在每个模型中忽略不同的列并测试效果。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建神经网络结构和模型&#40;数据挖掘中级教程&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的数据源视图](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
