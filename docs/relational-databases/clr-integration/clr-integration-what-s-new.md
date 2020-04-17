---
title: CLR 集成的新增功能 |微软文档
description: 托管 CLR 的 Microsoft SQL 服务器称为 CLR 集成。 本文介绍了 SQL Server 2012 中 CLR 集成中的新功能。
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: d27bf0d925d3a98dda488fb85aff7446434cc8ad
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488084"
---
# <a name="clr-integration---what39s-new"></a>CLR 集成 -&#39;新增功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  以下是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中 CLR 集成的新功能：  
  
-   在 CLR 版本 4 中，CLR 数据库对象不再捕获损坏的状态异常。 这些异常现在在 CLR 集成承载层中捕获。 CLR 数据库组件仍可以通过设置代码属性（[\<遗留的损坏状态异常策略>元素](https://go.microsoft.com/fwlink/?LinkId=204954)）来捕获这些异常。 但是，我们建议不要这样做，因为损坏的状态异常发生时结果不可靠。  
  
-   由于 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的严格安全要求，CLR 数据库组件将继续使用 CLR 版本 2.0 中定义的代码访问安全性模型。  
  
-   在 CLR 版本 4 中，系统中的格式错误 **。TimeSpan**值将生成**系统。** 在 CLR 版本 4 之前，系统 **.TimeSpan**值中的格式错误被忽略。 依赖于 CLR 版本 4 之前的行为的数据库应用程序应以 100 或更低的数据库兼容性级别 **（ALTER DATABASE 兼容性级别**） 运行。 有关详细信息，请参阅[<TimeSpan_LegacyFormatMode>元素](https://go.microsoft.com/fwlink/?LinkId=205109)。  
  
-   版本 4 的 CLR 支持 Unicode 5.1。 将会改善涉及一些重音记号和符号的排序操作。 如果您的应用程序依赖于旧的排序行为，可能会出现兼容性问题。 要启用旧排序，必须将数据库兼容性级别 **（ALTER 数据库兼容性级别**） 设置为 100 或更低。 为此，[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 将在 .NET Framework 4 目录 (C:\Windows\Microsoft.NET\Framework\v4.0.30319) 中安装 sort00001000.dll。 有关详细信息，请参阅[\<"比较排序">元素](https://go.microsoft.com/fwlink/?LinkId=205110)。  
  
-   以下列已添加到 sys [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md) **dm_clr_appdomains：total_processor_time_ms、total_allocated_memory_kb****total_allocated_memory_kb**和**survived_memory_kb**。  
  
  
