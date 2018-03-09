---
title: "SQL Server Management Studio - 遥测 (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 02/20/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
caps.latest.revision: "72"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a960b0862617027d77f28a7acc247312f461a78f
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="local-audit-for-ssms-usage-feedback-collection"></a>SSMS 使用反馈收集的本地审核
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] SQL Server Management Studio (SSMS) 包含支持 Internet 的功能，这些功能可收集并向 Microsoft 发送匿名功能使用情况数据。 SSMS 可能会收集标准计算机信息以及有关使用情况和性能的信息，并可能会将这些信息传输给 Microsoft 进行分析，以便改进 SSMS 的质量、安全性和可靠性。 我们不会收集您的姓名、地址或其他联系信息。 有关详细信息，请参阅 [SQL Server 隐私声明](https://www.microsoft.com/en-us/privacystatement/SQLServer/Default.aspx)。

## <a name="audit-feature-usage-data"></a>审核功能使用情况数据

若要查看 SSMS 收集的功能使用情况数据，请执行以下操作：
1.  启动 SSMS。
2.  单击“查看”，然后单击主菜单中的“输出”以显示“输出”窗口。 
3.  看到“输出”窗口后，选择“显示输出来源:”菜单中的“遥测”。

使用 SSMS 与数据库进行交互时，“输出”窗口显示收集的数据。

## <a name="enable-or-disable-usage-feedback-collection-in-ssms"></a>在 SSMS 中启用或禁用使用反馈收集

若要选择加入或退出 SSMS 的使用情况数据收集，请参阅：[如何将 SQL Server 2016 配置为向 Microsoft 发送反馈](http://support.microsoft.com/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft)。

## <a name="see-also"></a>另请参阅

[SQL Server 使用反馈收集的本地审核](http://msdn.microsoft.com/library/mt743085.aspx)
