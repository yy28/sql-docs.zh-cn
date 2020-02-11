---
title: 使用 Microsoft 商业智能 (BI) 工具进行分析和报告
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 7c76ec1a74032b5f35bc42ab4a901d95574e0900
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75688218"
---
# <a name="analysis-and-reporting-with-microsoft-business-intelligence-bi-tools"></a>使用 Microsoft 商业智能 (BI) 工具进行分析和报告

  下表将数据分析和报告的工作负荷映射到最适合这些工作负荷的 Microsoft BI 工具。  
  
 其目的是为了帮助您选择最能满足您需求的工具。 有关产品的详细信息，请单击表中的产品链接。  
  
 如果要查找这些工具的简短概述以帮助确定适合的工具，请参阅 [Microsoft Business Intelligence (BI) 工具简介](https://www.digitalvidya.com/blog/introduction-to-microsoft-power-bi/)。  
  
|工作负荷|用户|||BI 工具|||  
|---------------|----------|-|-|--------------|-|-|  
|||**Excel**|**SharePoint**|**SharePoint Online**|**Power BI**|**SQL Server**|  
|**自助服务 BI**|分析人员/最终用户||||||  
|方便地发现并访问公共和公司数据||[Power Query](https://go.microsoft.com/fwlink/p/?LinkId=391845)||[Azure 数据目录](https://azure.microsoft.com/services/data-catalog/)<br /><br />||  
|创建强大的数据模型||[Power Pivot](https://support.office.com/article/power-pivot-overview-and-learning-f9001958-7901-4caa-ad80-028a6d2432ed?ui=en-US&rs=en-US&ad=US)|||[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)||  
|执行自助式预测分析||||||[Excel 数据挖掘外接程序](../analysis-services/data-mining-client-for-excel-sql-server-data-mining-add-ins.md)|  
|可视化和浏览数据||[Power View](https://go.microsoft.com/fwlink/p/?LinkId=391847)<br /><br /> [三维地图](https://support.office.com/article/visualize-your-data-in-3d-maps-ce6b1d5c-4602-4dae-b487-91ec0268e75d)|||||  
|使用自然语言查询提问|||||[问 &](https://docs.microsoft.com/power-bi/consumer/end-user-q-and-a)||  
|使用移动设备访问报告||||[HTML 5 （支持查看 <10 MB 的文件）](https://go.microsoft.com/fwlink/p/?LinkId=391853)|[HTML 5 （支持查看 <250 MB）](https://go.microsoft.com/fwlink/p/?LinkId=391854)<br /><br /> [在 iOS 设备上 Power BI 移动应用](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-iphone-app-get-started)<br /><br /> [Android 设备上的 Power BI 移动应用](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-android-app-get-started) <br /><br />[适用于 Windows 10 的 Power BI 移动应用](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-windows-10-phone-app-get-started)||  
|协作和共享|||[SharePoint 站点](https://go.microsoft.com/fwlink/p/?LinkId=391849)|[SharePoint 团队网站](https://go.microsoft.com/fwlink/p/?LinkId=391850)|[Power BI 站点](https://docs.microsoft.com/power-bi/service-how-to-collaborate-distribute-dashboards-reports)||  
|**公司 BI**|IT 专家||||||  
|创建多维/表格公司模型||||||[Analysis Services](https://docs.microsoft.com/analysis-services/analysis-services-overview)|  
|创建即席数据可视化|||[Power View for SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=391858)||||  
|创建面板|||[SharePoint 面板](https://go.microsoft.com/fwlink/p/?LinkId=391859)<br /><br /> [PerformancePoint 服务](https://technet.microsoft.com/library/ee424392.aspx)||||  
|创建操作报表||||||<sup>1</sup> [Reporting Services](create-deploy-and-manage-mobile-and-paginated-reports.md)|  
|创建自定义和嵌入式报表||||||<sup>1</sup> [Reporting Services](create-deploy-and-manage-mobile-and-paginated-reports.md)|  
|**高级分析**|数据科学家||||||  
|执行自助式预测分析||||||[Excel 数据挖掘外接程序](https://msdn.microsoft.com/library/dn282385\(v=sql.120\).aspx)|  
|使用数据挖掘算法||||||[Analysis Services 中的数据挖掘](https://technet.microsoft.com/library/bb510516\(v=sql.120\).aspx)|  
  
 <sup>1</sup> Reporting Services 提供多种功能，这些功能支持交付操作报表和自定义报表，如订阅和数据警报。