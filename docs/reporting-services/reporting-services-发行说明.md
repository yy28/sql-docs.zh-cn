---
title: "SSRS 中的 Power BI 技术预览版报表 - 发行说明 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f20d7-a9f9-47e3-8dc3-c544a14457e0
caps.latest.revision: 5
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Reporting Services 发行说明
 ||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  SQL Server Reporting Services 中 2017 年 1 月的 Power BI 技术预览版报表|

本主题介绍了 SQL Server Reporting Services 中 Power BI 技术预览版报表存在的限制和问题。

- 若要了解此版本中的新增功能，请参阅 [Reporting Services 中的新增功能](../reporting-services/sql-server-reporting-services-ssrs-中的新增功能.md)。

 **进行试用：**    
   -   [![从 Microsoft 下载中心进行下载](../analysis-services/media/download.png)](https://go.microsoft.com/fwlink/?linkid=839351)  从 **[Microsoft 下载中心](https://go.microsoft.com/fwlink/?linkid=839351)**下载 SQL Server Reporting Services 中的 Power BI 技术预览版报表以及 Power BI Desktop (SQL Server Reporting Services)


## <a name="january--2017"></a>2017 年 1 月

### <a name="report-server"></a>报表服务器

- 现支持 Https。 在 2016 年 10 月发布的技术预版 VM 中尚未提供此支持。 有关详细信息，请参阅[配置本机模式报表服务器上的 SSL 连接](../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。
   - 要使用 PowerPoint Web 查看器外接程序并在其中公开 Power BI 报表，Https 是必需的。
- 现支持扩展。 在 2016 年 10 月发布的技术预版 VM 中尚未提供此支持。 有关详细信息，请参阅[配置本机模式报表服务器扩展部署](../reporting-services/install-windows/configure a native mode report server scale-out deployment.md)。

### <a name="power-bi-reports"></a>Power BI 报表

- 必须使用 Power BI Desktop (SQL Server Reporting Services) 创建 Power BI 报表，才能通过 SQL Server Reporting Services 对其进行处理。 可从评估中心下载 Power BI Desktop (SQL Server Reporting Services)。
- Power BI 报表仅支持与 Analysis Services （表格或多维）进行实时连接。
- 不支持自定义视觉对象。
- 不支持 R 视觉对象。