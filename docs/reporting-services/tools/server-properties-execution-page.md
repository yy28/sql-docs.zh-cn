---
title: "服务器属性 （执行页） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.execution.f1
ms.assetid: 53b77db1-b013-4dac-82dd-30c0de276639
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 933f3287d8e02df8aeadf93bbd7ce39f20aff268
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="server-properties-execution-page"></a>服务器属性（“执行”页）
  使用此页可设置报表执行的超时值。 此值将应用于当前报表服务器实例处理的所有报表。 您可以针对单个报表覆盖此值。 您指定的值必须适合报表服务器上发生的所有报表处理，并适合在报表服务器检索报表中所使用的数据时针对数据库服务器执行的查询处理。  
  
 若要打开此页，请启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，连接到报表服务器实例，右键单击报表服务器名称，然后选择“属性”。 单击 **“执行”** 将此页打开。  
  
## <a name="options"></a>选项  
 **不对报表执行时间设置超时**  
 允许报表服务器在不受限制的时间内完成报表处理。  
  
 **将报表执行时间限制为(以秒计)**  
 针对报表执行设置时间约束。 在请求报表时将对该时间段开始计时。 如果在报表处理全部完成之前该时间段就已结束，那么报表服务器将取消该处理和所有对外部数据源的处理中的查询。  
  
## <a name="see-also"></a>另请参阅  
 [设置报表服务器属性 &#40;Management Studio &#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [连接到在 Management Studio 中的报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [设置报表处理属性](../../reporting-services/report-server/set-report-processing-properties.md)   
 [报表和共享数据集处理 &#40; 设置超时值SSRS &#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)   
 [Management Studio F1 帮助中的报表服务器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  

