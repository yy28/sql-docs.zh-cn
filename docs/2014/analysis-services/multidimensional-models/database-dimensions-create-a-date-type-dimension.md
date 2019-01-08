---
title: 创建日期类型维度 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time dimensions [Analysis Services]
- dimensions [Analysis Services], time
- adding time intelligence
- server time dimensions [Analysis Services]
- calendars [Analysis Services]
- time intelligence [Analysis Services]
ms.assetid: 6d692856-4b01-4dca-a650-f97ac220c114
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3eec8ddf87193eddbafc5a56e8e397c83f142a91
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513074"
---
# <a name="create-a-date-type-dimension"></a>创建日期类型维度
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，时间维度是指其属性表示时间段（如年、半期、季度、月和天）的维度类型。 时间维度中的时间段可提供用于分析和报告的基于时间的粒度级别。 属性将按层次结构进行组织，并且时间维度的粒度主要由历史数据的业务和报表需求决定。 例如，商业智能应用程序中的大多数财务数据和销售数据使用月粒度或季度粒度。  
  
 通常， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的多维数据集会以某种形式合并一个时间维度。 多维数据集可能包含多个时间维度，也可以包含来自同一时间维度的多个层次结构，具体将取决于数据的粒度和报表需求。 但是，并非所有多维数据集都需要时间维度。 某些 OLAP 应用程序（例如，基于活动的开销）不需要时间维度，因为基于活动的维度内的开销是基于活动的，而不是基于时间的。  
  
## <a name="dimension-structure"></a>维度结构  
 时间维度的维度结构将取决于基础数据源存储时间段信息的方式。 按照存储方式的不同，时间维度具有以下两种基本类型：  
  
 时间维度  
 与其他维度相似，时间维度也使用维度表提供维度属性。 维度主表中的每一列定义一个特定时间段的属性。  
  
 与其他维度类似，事实数据表与时间维度的维度表之间同样存在一个外键关系。 时间维度的键属性基于整型键或最低级别的详细信息，如出现在维度主表中的日期。  
  
 服务器时间维度  
 如果没有要将时间相关属性绑定到的维度表，则可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 基于时间段定义一个服务器时间维度。 若要定义由服务器时间维度表示的层次结构、级别和成员，应当在创建维度时选择标准时间段。  
  
 服务器时间维度中的属性具有特殊的时间-属性绑定。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用与日期相关的属性类型（例如，年、月或天）来定义时间维度中的属性成员。  
  
 在多维数据集中包含了服务器时间维度之后，可通过在多维数据集向导的 **“定义维度用法”** 页中指定一个关系，以建立度量值组和服务器时间维度之间的关系。  
  
### <a name="calendars"></a>日历  
 在时间维度或服务器时间维度中，时间段属性在层次结构中将组合在一起进行分组。 此类层次结构通常称为日历。  
  
 商业智能应用程序经常需要多个日历定义。 例如，人力资源部门可能使用跟踪雇员*标准*日历的十二个月的公历月 1 日开始到年 12 月 31 日结束。 但是，同一人力资源部门可能使用跟踪支出*会计*日历的十二个月的日历，定义组织使用的会计年度。  
  
 可以在维度设计器中手动构造这些不同的日历。 但是，在创建时间维度或服务器时间维度时，维度向导会提供几个层次结构模板，可用于自动生成若干种类型的日历。 下表说明了可通过维度向导生成的各种日历。  
  
|Calendar|Description|  
|--------------|-----------------|  
|标准日历|十二个月的公历，从 1 月 1 日开始，到 12 月 31 日结束。<br /><br /> 无论使用维度向导创建时间维度还是服务器时间维度，在定义了表示维度的时间段属性之后，该向导都会生成一个标准日历的层次结构。 如果使用维度向导创建服务器时间维度，则可将标准日历的开始日期调整为 1 月 1 日以外的某一天。|  
|会计日历|十二个月会计日历。 如果选择该日历，则要为单位使用的会计日历指定开始的月份和日期。<br /><br /> 注意：只有在使用维度向导创建服务器时间维度时，该日历才可用。|  
|报表日历（或营销日历）|十二个月的报表日历，在该日历以三个月（每季度）重复的模式中，其中两个月为四周，一个月为五周。 选择该日历时, 指定的开始日期和月份和 4-4-5、 4-5-4 或 5-4-4 周，其中每个数字表示在一个月的周数的三个月模式。<br /><br /> 注意：只有在使用维度向导创建服务器时间维度时，该日历才可用。|  
|生产日历|该日历使用 13 个为时四周的期间，其中有三个季度每个季度包含三个期间，一个季度包含四个期间。 如果使用该日历，则要为单位使用的生产年度指定开始周（1 到 4 之间）和月份，并标识出包含四个期间的季度。<br /><br /> 注意：只有在使用维度向导创建服务器时间维度时，该日历才可用。|  
|ISO 8601 日历|国际标准化组织 (ISO) 的日期和时间标准日历的表示法 (8601)。 该日历具有整数个为时 7 天的周。 该日历新年的开始日期可能比公历新年的开始日期早或晚几天。 该日历的第一周根据公历的包含星期四的第一个周进行确定。 因此，该周的第一天（周日）可能会从上一年开始。<br /><br /> 注意：只有在使用维度向导创建服务器时间维度时，该日历才可用。|  
  
 创建服务器时间维度，并指定在该维度中要使用的时间段和日历时，维度向导将为每个指定日历的相应时间段添加属性。 例如，如果创建的服务器时间维度使用年作为时间段，并同时包括会计和报表日历，则向导会将 FiscalYear 和 ReportingYears 属性与标准 Years 属性一起添加到维度中。 服务器时间维度还具有选定时间段组合的属性，如包含天数和周数的维度的 DayOfWeek 属性。 维度向导通过将属于一种日历类型的属性组合起来，据以创建日历层次结构。 例如，会计日历层次结构可能包含以下级别：会计年度、 会计半年、 会计季度、 会计月份和某一会计日。  
  
## <a name="adding-time-intelligence-with-the-business-intelligence-wizard"></a>使用商业智能向导添加时间智能。  
 定义时间维度并将该维度添加到多维数据集之后，可以使用商业智能向导添加时间智能功能，如“本期截止到现在”、“期间到期间”以及“移动平均”等度量值。 有关详细信息，请参阅 [使用商业智能向导定义时间智能计算](define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)。  
  
> [!NOTE]  
>  您不能使用商业智能向导向服务器时间维度中添加时间智能。 商业智能向导添加了一个支持时间智能的层次结构，必须将此层次结构绑定到时间维度表的某个列。 服务器时间维度没有对应的时间维度表，因此无法支持这个附加的层次结构。  
  
## <a name="see-also"></a>请参阅  
 [通过生成时间表来创建时间维度](create-a-time-dimension-by-generating-a-time-table.md)   
 [商业智能向导的 F1 帮助](../business-intelligence-wizard-f1-help.md)   
 [维度类型](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
