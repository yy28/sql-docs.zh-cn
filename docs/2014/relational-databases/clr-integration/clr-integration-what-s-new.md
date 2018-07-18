---
title: 什么&#39;CLR 集成中的新增功能的 s |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
caps.latest.revision: 6
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 47566d2f3557202370a1b6be25a759f9cea3af17
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37352499"
---
# <a name="what39s-new-in-clr-integration"></a>什么&#39;s CLR 集成中的新增功能
  以下是 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中 CLR 集成的新功能：  
  
-   在 CLR 版本 4 中，CLR 数据库对象不再捕获损坏的状态异常。 这些异常现在在 CLR 集成承载层中捕获。 这些异常仍可以捕获由 CLR 数据库组件通过设置代码属性 ([\<legacyCorruptedStateExceptionsPolicy > 元素](http://go.microsoft.com/fwlink/?LinkId=204954))。 但是，我们建议不要这样做，因为损坏的状态异常发生时结果不可靠。  
  
-   由于 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 的严格安全要求，CLR 数据库组件将继续使用 CLR 版本 2.0 中定义的代码访问安全性模型。  
  
-   在 CLR 版本 4 中，`System.TimeSpan` 值中的格式错误将生成 `System.FormatExceptions`。 在 CLR 版本 4 之前，忽略 `System.TimeSpan` 值中的格式错误。 依赖于 CLR 版本 4 之前的行为的数据库应用程序应使用数据库兼容级别 (`ALTER DATABASE Compatibility Level`) 100 或更低来运行。 有关详细信息，请参阅[< TimeSpan_LegacyFormatMode > 元素](http://go.microsoft.com/fwlink/?LinkId=205109)。  
  
-   版本 4 的 CLR 支持 Unicode 5.1。 将会改善涉及一些重音记号和符号的排序操作。 如果您的应用程序依赖于旧的排序行为，可能会出现兼容性问题。 若要启用旧的排序，必须将数据库兼容级别 (`ALTER DATABASE Compatibility Level`) 设置为 100 或更低。 为此，[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 将在 .NET Framework 4 目录 (C:\Windows\Microsoft.NET\Framework\v4.0.30319) 中安装 sort00001000.dll。 有关详细信息，请参阅[ \<CompatSortNLSVersion > 元素](http://go.microsoft.com/fwlink/?LinkId=205110)。  
  
-   以下各列已添加到[sys.dm_clr_appdomains](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql): `total_processor_time_ms`， `total_allocated_memory_kb`，和`survived_memory_kb`。  
  
  
