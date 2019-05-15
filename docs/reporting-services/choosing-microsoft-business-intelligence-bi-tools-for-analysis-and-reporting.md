---
title: 使用 Microsoft 商业智能 (BI) 工具进行分析和报告
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services, sql-server
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 7916d3b2afe514d576ba7ec99cd1a7edab244278
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503904"
---
# <a name="analysis-and-reporting-with-microsoft-business-intelligence-bi-tools"></a>使用 Microsoft 商业智能 (BI) 工具进行分析和报告

选择正确的商业智能工具可能令人难以应付。 了解不同 Microsoft 产品，找到最适合你需求的一个产品。

下表将数据分析和报告的工作负荷映射到最适合这些工作负荷的 Microsoft BI 工具。 有关产品的详细信息，请单击表中的产品链接。  
  
 如果要查找这些工具的简短概述以帮助确定适合的工具，请参阅 [Microsoft Business Intelligence (BI) 工具简介](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Introducing_Microsoft_BI_Tools.docx)。

> [!NOTE]
> 自 SQL Server 2016 之后，不再提供 Reporting Services 与 SharePoint 的集成这一功能。
  
|工作负荷|用户|||BI 工具|||  
|---------------|----------|-|-|--------------|-|-|  
|||**Excel**|**SharePoint**|**SharePoint Online**|**Power BI**|**SQL Server**|  
|**自助式 BI**|分析人员/最终用户||||||  
|方便地发现并访问公共和公司数据||[Excel 2016](https://support.office.com/article/What-s-new-in-Excel-2016-for-Windows-5fdb9208-ff33-45b6-9e08-1f5cdb3a6c73?ui=en-US&rs=en-US&ad=US)|||[Azure 数据目录](https://azure.microsoft.com/services/data-catalog/)||  
|创建强大的数据模型||[Power Pivot](https://support.office.com/article/Power-Pivot-Overview-and-Learning-f9001958-7901-4caa-ad80-028a6d2432ed?ui=en-US&rs=en-US&ad=US)|||[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)||  
|执行自助式预测分析||||||[Excel 数据挖掘外接程序](https://docs.microsoft.com/sql/analysis-services/data-mining-client-for-excel-sql-server-data-mining-add-ins?view=sql-server-2014&viewFallbackFrom=sql-server-ver15) |  
|可视化和浏览数据||[Power View](https://support.office.com/article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e)<br /><br /> [三维地图](https://support.office.com/article/Visualize-your-data-in-3D-Maps-ce6b1d5c-4602-4dae-b487-91ec0268e75d)|||[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)||  
|使用自然语言查询提问|||||[问答](https://docs.microsoft.com/power-bi/consumer/end-user-q-and-a)|
|使用移动设备访问报告||||[HTML 5（支持查看 10 MB 以内的文件）](create-deploy-and-manage-mobile-and-paginated-reports.md)<br /><br /> | [HTML 5（支持查看 250 MB 以内的文件）](http://go.microsoft.com/fwlink/p/?LinkId=391854)<br /><br /> [iOS 设备上的 Power BI 移动应用](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-iphone-app-get-started)<br /><br /> [Android 设备上的 Power BI 移动应用](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-android-app-get-started) <br /><br /> [适用于 Windows 10 的 Power BI 移动应用](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-windows-10-phone-app-get-started)|  
|协作和共享|||[SharePoint 网站](https://docs.microsoft.com/sharepoint/getting-started)|[SharePoint 团队网站](https://go.microsoft.com/fwlink/?LinkId=391850)|[Power BI 网站](https://docs.microsoft.com/power-bi/service-how-to-collaborate-distribute-dashboards-reports)||  
|**公司 BI**|IT 专业人员||||||  
|创建多维/表格公司模型||||||[Analysis Services](../analysis-services/analysis-services.md)|  
|创建即席数据可视化|||[Power View for SharePoint](https://go.microsoft.com/fwlink/?LinkId=391858)||||  
|创建面板|||[SharePoint 面板](https://go.microsoft.com/fwlink/?LinkId=391859)<br /><br /> [PerformancePoint 服务](https://technet.microsoft.com/library/ee424392.aspx)||[Power BI 中的仪表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)||  
|创建操作报表||||||*[Reporting Services](create-deploy-and-manage-mobile-and-paginated-reports.md)|  
|创建自定义和嵌入式报表|||||[Power BI Embedded](create-deploy-and-manage-mobile-and-paginated-reports.md)|  
|**高级分析**|数据科学家||||||  
|执行自助式预测分析||||||[Excel 数据挖掘外接程序](https://docs.microsoft.com/sql/analysis-services/data-mining-client-for-excel-sql-server-data-mining-add-ins?view=sql-server-2014&viewFallbackFrom=sql-server-ver15) |  
|使用数据挖掘算法||||||[Analysis Services 中的数据挖掘](../analysis-services/data-mining/data-mining-ssas.md)<br/><br/>[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)|  
  
 *Reporting Services 具有大量支持交付操作报表和自定义报表的功能，如交付新式分页报表。