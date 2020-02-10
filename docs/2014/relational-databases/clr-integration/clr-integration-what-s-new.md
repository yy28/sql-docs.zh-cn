---
title: CLR 集成中的新增&#39;Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 45e4f0578d06eeafc545bea2b6374a37b8ef7cbc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874075"
---
# <a name="what39s-new-in-clr-integration"></a>CLR 集成中的新增功能&#39;
  以下是 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中 CLR 集成的新功能：  
  
-   在 CLR 版本 4 中，CLR 数据库对象不再捕获损坏的状态异常。 这些异常现在在 CLR 集成承载层中捕获。 CLR 数据库组件仍可以通过设置代码属性（[\<legacyCorruptedStateExceptionsPolicy> 元素](https://go.microsoft.com/fwlink/?LinkId=204954)）捕获这些异常。 但是，我们建议不要这样做，因为损坏的状态异常发生时结果不可靠。  
  
-   由于 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 的严格安全要求，CLR 数据库组件将继续使用 CLR 版本 2.0 中定义的代码访问安全性模型。  
  
-   在 CLR 版本 4 中，`System.TimeSpan` 值中的格式错误将生成 `System.FormatExceptions`。 在 CLR 版本 4 之前，忽略 `System.TimeSpan` 值中的格式错误。 依赖于 CLR 版本 4 之前的行为的数据库应用程序应使用数据库兼容级别 (`ALTER DATABASE Compatibility Level`) 100 或更低来运行。 有关详细信息，请参阅[<TimeSpan_LegacyFormatMode> 元素](https://go.microsoft.com/fwlink/?LinkId=205109)。  
  
-   版本 4 的 CLR 支持 Unicode 5.1。 将会改善涉及一些重音记号和符号的排序操作。 如果您的应用程序依赖于旧的排序行为，可能会出现兼容性问题。 若要启用旧的排序，必须将数据库兼容级别 (`ALTER DATABASE Compatibility Level`) 设置为 100 或更低。 为此，[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 将在 .NET Framework 4 目录 (C:\Windows\Microsoft.NET\Framework\v4.0.30319) 中安装 sort00001000.dll。 有关详细信息，请参阅[ \<CompatSortNLSVersion> 元素](https://go.microsoft.com/fwlink/?LinkId=205110)。  
  
-   以下列已添加到[sys.databases dm_clr_appdomains](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql)： `total_processor_time_ms`、 `total_allocated_memory_kb`和`survived_memory_kb`。  
  
  
