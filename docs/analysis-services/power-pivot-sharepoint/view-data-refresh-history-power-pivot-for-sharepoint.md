---
title: "查看数据刷新历史记录 (Power Pivot for SharePoint) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- data refresh history [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 4c8d8aa8-794d-4f72-ace3-78d0e688e1a5
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fc4dcd60f4a37b1b3f01844369f210a81653160b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="view-data-refresh-history-power-pivot-for-sharepoint"></a>查看数据刷新历史记录 (Power Pivot for SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]数据刷新历史记录是指的所有数据刷新活动记录[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]Excel 工作簿中的数据。 将根据您提供的计划，对 SharePoint 场中的 Analysis Services 服务器实例执行数据刷新操作。 默认情况下，数据刷新历史记录将保留一年时间。 但是，场管理员可以为使用情况和事件历史记录指定不同的保持策略，以确定将数据刷新记录保留多长时间。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **本主题内容：**  
  
 [先决条件](#prereq)  
  
 [查看单独工作簿的数据刷新历史记录](#viewhistory)  
  
 [查看所有工作簿的数据刷新历史记录](#viewITOps)  
  
 [使用历史记录信息](#pageelements)  
  
##  <a name="prereq"></a> 先决条件  
 您必须具有“参与讨论”权限或更高权限，才能查看数据刷新历史记录。  
  
 你必须已启用和计划对包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的工作簿进行数据刷新。 如果您未计划数据刷新，您将看到计划定义页，而不是历史记录信息。  
  
##  <a name="viewhistory"></a> 查看单独工作簿的数据刷新历史记录  
  
1.  在 SharePoint 站点上，打开一个包含 Excel 工作簿（其中包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据）的库。  
  
     没有可视的指示器用于标识 SharePoint 库中的哪些工作簿包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据。 你必须预先知道哪些工作簿包含可刷新的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据。  
  
2.  选择工作簿，然后单击显示在右侧的向下箭头。  
  
3.  选择“管理 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据刷新”。  
  
 将出现历史记录页，其中显示当前 Excel 工作簿中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的所有刷新活动的完整记录。  
  
##  <a name="viewITOps"></a> 查看所有工作簿的数据刷新历史记录  
 通过使用管理中心中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理面板，场管理员和服务应用程序管理员可全面了解所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿的数据刷新历史记录和状态。 有关详细信息，请参阅 [Power Pivot Management Dashboard and Usage Data](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)。  
  
##  <a name="pageelements"></a> 使用历史记录信息  
 数据刷新历史记录页提供有关每个刷新操作的详细信息。 可以使用此页上的信息来确认是否发生了刷新或确定失败原因。  
  
|项|Description|  
|----------|-----------------|  
|“属性”|指定包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的 Excel 工作簿的文件名。|  
|当前状态|值包括 **“已计划”**、 **“正在刷新”**、 **“成功”**或 **“失败”**。<br /><br /> 当您首次创建计划时，将显示**“已计划”** 。 在首次运行数据刷新后，将不再显示此状态消息。<br /><br /> **“正在刷新”** 表示正在进行数据刷新。 请求位于进程队列中或当前正在服务器上运行。<br /><br /> **“成功”** 表示最后一个数据刷新操作已完成，并且已将更新的工作簿签回到 SharePoint 库中。<br /><br /> **“失败”** 表示最后一个数据刷新操作未成功。 刷新的数据未保存。 工作簿与开始刷新数据之前包含相同的数据。|  
|最近成功刷新|指定成功完成最后一次数据刷新的日期。|  
|下次计划刷新|指定计划进行的下一次数据刷新的日期。<br /><br /> **“配置计划”** 链接将您引向计划定义页。 如果你对工作簿具有“参与讨论”权限，可以单击此链接，以查看和修改控制工作簿中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的无人参与数据刷新的计划信息。|  
|Started|在历史记录详细信息部分中， **“已启动”** 表示实际的处理时间。 实际的处理时间可能与您计划的时间不同。 当服务器上有足够的内存时，将开始处理。 如果服务器很忙，处理过程可能在您指定的开始时间之后的若干小时才开始。|  
|已完成|在历史记录详细信息部分中， **“已完成”** 指示完成数据刷新操作的时间。 此日期和时间表示将工作簿检回到库中的时间。<br /><br /> 如果数据刷新失败，将显示一条或多条错误消息来说明失败的原因。 您可以展开每条记录，以查看详细状态。 将单独列出每个数据源，以及成功消息或解释数据刷新为何未完成的失败消息。|  
|Time|提供从开始数据刷新到完成刷新的累计时间。|  
|“登录属性”|提供有关刷新操作是成功还是失败的历史记录。|  
  
## <a name="see-also"></a>另请参阅  
 [配置使用情况数据收集 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [计划数据刷新 (Power Pivot for SharePoint)](http://msdn.microsoft.com/en-us/8571208f-6aae-4058-83c6-9f916f5e2f9b)   
 [Power Pivot 数据刷新](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  
