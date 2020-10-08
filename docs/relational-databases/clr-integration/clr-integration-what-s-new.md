---
title: CLR 集成中的新增功能 |Microsoft Docs
description: 承载 CLR Microsoft SQL Server 称为 CLR 集成。 本文介绍 SQL Server 2012 的 CLR 集成中的新增功能。
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: eaf16cda98f019f6d378a3287e1068d78df88bac
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809513"
---
# <a name="clr-integration---what39s-new"></a>CLR 集成-新增&#39;
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  以下是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中 CLR 集成的新功能：  
  
-   在 CLR 版本 4 中，CLR 数据库对象不再捕获损坏的状态异常。 这些异常现在在 CLR 集成承载层中捕获。 CLR 数据库组件仍可以通过将代码特性设置 ([ \<legacyCorruptedStateExceptionsPolicy> 元素](/dotnet/framework/configure-apps/file-schema/runtime/legacycorruptedstateexceptionspolicy-element)) 来捕获这些异常。 但是，我们建议不要这样做，因为损坏的状态异常发生时结果不可靠。  
  
-   由于 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的严格安全要求，CLR 数据库组件将继续使用 CLR 版本 2.0 中定义的代码访问安全性模型。  
  
-   在 CLR 版本4中， **系统. TimeSpan** 值中的格式错误将生成 **FormatExceptions**。 在 CLR 版本4之前，系统中出现格式错误 **。 TimeSpan** 值被忽略。 依赖于 CLR 版本4之前的行为的数据库应用程序应使用数据库兼容性级别运行 (**更改数据库兼容性级别**) 为100或更低版本。 有关详细信息，请参阅 [<TimeSpan_LegacyFormatMode> 元素](/dotnet/framework/configure-apps/file-schema/runtime/timespan-legacyformatmode-element)。  
  
-   版本 4 的 CLR 支持 Unicode 5.1。 将会改善涉及一些重音记号和符号的排序操作。 如果您的应用程序依赖于旧的排序行为，可能会出现兼容性问题。 若要启用旧排序，数据库兼容性级别 (**ALTER Database 兼容级别**) 必须设置为100或更低。 为此，[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 将在 .NET Framework 4 目录 (C:\Windows\Microsoft.NET\Framework\v4.0.30319) 中安装 sort00001000.dll。 有关详细信息，请参阅 [\<CompatSortNLSVersion> 元素](/dotnet/framework/configure-apps/file-schema/runtime/compatsortnlsversion-element)。  
  
-   已将以下各列添加到 [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)： **total_processor_time_ms**、 **total_allocated_memory_kb**和 **survived_memory_kb**。  
  
