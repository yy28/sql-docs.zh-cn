---
title: "什么 &#39; s CLR 集成中的新增功能 |Microsoft 文档"
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 787552c5a10579e90a0ab62e9105172f989357f5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="clr-integration---what39s-new"></a>CLR 集成的新增功能; s 新
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]以下是中的 CLR 集成中的新增功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   在 CLR 版本 4 中，CLR 数据库对象不再捕获损坏的状态异常。 这些异常现在在 CLR 集成承载层中捕获。 这些异常仍由 CLR 数据库组件通过设置 code 属性捕获 ([\<legacyCorruptedStateExceptionsPolicy > 元素](http://go.microsoft.com/fwlink/?LinkId=204954))。 但是，我们建议不要这样做，因为损坏的状态异常发生时结果不可靠。  
  
-   由于 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的严格安全要求，CLR 数据库组件将继续使用 CLR 版本 2.0 中定义的代码访问安全性模型。  
  
-   在 CLR 版本 4 中的格式错误**System.TimeSpan**值将生成**System.FormatExceptions**。 之前的版本 4 的 CLR 中的格式错误**System.TimeSpan**值被忽略。 数据库应用程序依赖于之前的 CLR 版本 4 的行为应运行与数据库兼容性级别 (**ALTER DATABASE 兼容级别**) 为 100 或更低。 有关详细信息，请参阅[< TimeSpan_LegacyFormatMode > 元素](http://go.microsoft.com/fwlink/?LinkId=205109)。  
  
-   版本 4 的 CLR 支持 Unicode 5.1。 将会改善涉及一些重音记号和符号的排序操作。 如果您的应用程序依赖于旧的排序行为，可能会出现兼容性问题。 若要启用旧排序，数据库兼容级别 (**ALTER DATABASE 兼容级别**) 必须设置为 100 或更低。 为此，[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 将在 .NET Framework 4 目录 (C:\Windows\Microsoft.NET\Framework\v4.0.30319) 中安装 sort00001000.dll。 有关详细信息，请参阅[ \<CompatSortNLSVersion > 元素](http://go.microsoft.com/fwlink/?LinkId=205110)。  
  
-   下面的列已添加到[sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**， **total_allocated_memory_kb**，和**survived_memory_kb**。  
  
  
