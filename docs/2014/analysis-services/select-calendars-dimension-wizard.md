---
title: 选择日历 （维度向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.serverSpecialCalendars.f1
ms.assetid: 6e28a020-2586-4b13-9333-b499fb1b33af
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 67e4d316b122f44e207037603354f696446aed3f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48139437"
---
# <a name="select-calendars-dimension-wizard"></a>选择日历（维度向导）
  可以使用“选择日历”页，为时间维度创建表示会计、报表、生产或国际标准化组织 (ISO) 8601 日历的其他层次结构。  
  
> [!NOTE]  
>  只有在“选择维度类型”页上选择“服务器时间维度”，或者在“维度定义”页上选择“不使用数据源生成维度”并在“选择维度类型”页上选择“时间维度”时，才会显示此页。  
  
## <a name="options"></a>选项  
 **会计日历**  
 选择此选项可以基于会计日历创建时间层次结构。  
  
 **起始日和月份**  
 选择会计日历开始的日期和月份。  
  
> [!NOTE]  
>  只有在选择了“会计日历”时，此选项才可用。  
  
 **会计日历命名约定**  
 选择会计日历使用的命名约定。 选择“日历年名称”或“日历年名称 + 1”。  
  
> [!NOTE]  
>  只有在选择了“会计日历”时，此选项才可用。  
  
 **报表 （或营销） 日历**  
 选择此项可以基于报表日历创建时间层次结构。  
  
 **起始周和月份**  
 选择报表日历开始的周和月份。  
  
> [!NOTE]  
>  只有在选择了“报表(或营销)日历”时，此选项才可用。  
  
 **月份周别模式**  
 选择报表日历使用的月份周别模式。  
  
> [!NOTE]  
>  只有在选择了“报表(或营销)日历”时，此选项才可用。  
  
 下表列出了月份周别模式可用的选项：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**一周 445**|季度的第一个月有 4 周，第二个月有 4 周，第三个月有 5 周。|  
|**一周 454**|季度的第一个月有 4 周，第二个月有 5 周，第三个月有 4 周。|  
|**一周 544**|季度的第一个月有 5 周，第二个月有 4 周，第三个月有 4 周。|  
  
 **生产日历**  
 选择此项可以基于生产日历创建时间层次结构。  
  
 **起始周和月份**  
 选择生产日历开始的周和月份。  
  
> [!NOTE]  
>  只有在选择了“生产日历”时，此选项才可用。  
  
 **包含附加期间的季度**  
 选择或键入将包含附加期间的季度。  
  
> [!NOTE]  
>  只有在选择了“生产日历”时，此选项才可用。  
  
 **ISO 8601 日历**  
 选择此项可以基于 ISO 8601 日历创建层次结构。  
  
## <a name="see-also"></a>请参阅  
 [维度向导的 F1 帮助](dimension-wizard-f1-help.md)   
 [维度&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
