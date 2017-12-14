---
title: SQL Server Integration Services | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
keywords: SSIS
helpviewer_keywords:
- SSIS
- DTS [Integration Services]
- SQL Server Integration Services
- Integration Services
- DTS [Integration Services], about Integration Services
- data integration [Integration Services]
- Data Transformation Services
ms.assetid: c4398655-5657-4ae4-a690-a380790fe84f
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 812980a1fffc05c40531cb961502ec2b627fd402
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="sql-server-integration-services"></a>SQL Server Integration Services

 > 有关与 SQL Server 早期版本相关的内容，请参阅 [SQL Server Integration Services](https://msdn.microsoft.com/library/ms141026(SQL.120).aspx)。

[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是用于生成企业级数据集成和数据转换解决方案的平台。 使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 可解决复杂的业务问题，具体表现为：复制或下载文件，发送电子邮件以响应事件，更新数据仓库，清除和挖掘数据以及管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 对象和数据。 这些包可以独立使用，也可以与其他包一起使用以满足复杂的业务需求。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 可以提取和转换来自多种源（如 XML 数据文件、平面文件和关系数据源）的数据，然后将这些数据加载到一个或多个目标。<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含一组丰富的内置任务和转换、用于构造包的工具以及用于运行和管理包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务。 可以使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 图形工具来创建解决方案，而无需编写一行代码；也可以对各种 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型进行编程，通过编程方式创建包并编写自定义任务以及其他包对象的代码。

## <a name="try-sql-server-and-sql-server-integration-services"></a>试用 SQL Server 和 SQL Server Integration Services
- [![从评估中心下载](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477) [下载 SQL Server 2017 或 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server)
- [![从评估中心下载](../includes/media/download2.png)](../ssdt/download-sql-server-data-tools-ssdt.md) [下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- [![从评估中心下载](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) [下载 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)

##  <a name="infotipsql-servermediainfo-tippng-get-help"></a>![info_tip](../sql-server/media/info-tip.png) 获取帮助
 
- [关于 SSIS 的 MSDN 论坛 - 提出问题](https://social.msdn.microsoft.com/Forums/home?forum=sqlintegrationservices)
- [关于 SSDT 和 SSMS 的 MSDN 论坛 - 提出问题](https://social.msdn.microsoft.com/Forums/home?forum=sqltool)
- [Stack Overflow（标记 *ssis*）- 提出问题](http://stackoverflow.com/questions/tagged/ssis)
- [Microsoft Connect - 报告 bug 和请求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有关 SSIS 的一般讨论](https://www.reddit.com/r/SQLServer/search?q=ssis&restrict_sr=on)
- [Microsoft 企业用户支持选项](https://support.microsoft.com/gp/support-options-for-business)
- [面向企业用户的“联系 Microsoft”选项](https://support.microsoft.com/gp/contactus81?Audience=Commercial)
