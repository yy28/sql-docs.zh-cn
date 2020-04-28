---
title: 驱动程序版本方案 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 864a8bd892315b060fc6fcf42dbe69dfea61ae59
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303448"
---
# <a name="driver-version-scheme"></a>驱动程序版本方案
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 下表列出了适用于 Oracle 的 Microsoft ODBC 驱动程序的所有发行版。  
  
|驱动程序版本|生成号|可用性历史记录|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 和 Visual Basic 5.0，Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 和 MDAC 1.5 a|  
|2.0 更新|2.73.7283.01|IIS 4。0|  
|2.0 更新|2.73.7283.03|MDAC 1.5 b 和 1.5 c|  
|2.0 更新|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 和 MDAC 2。0|  
|2.5 更新|2.573.3513|SQL Server 7。0<br /><br /> SQL Server 6.5 SP5|  
  
 Build 2.00.6235 （版本1）是 Microsoft ODBC Driver for Oracle 的第一个版本。 第一版发布后，采用新的命名约定。  
  
 例如，可以将2.73.7283.03 划分为以下不同的组件：  
  
-   2 = 版本号。  
  
-   73 = 为其设计驱动程序的 Oracle 服务器的版本。  
  
-   7283.03 = 驱动程序的生成号。  
  
> [!NOTE]  
>  使用 release 2.573.2973，命名约定导致了一些混乱，2.573 是比2.73 更早的版本，但生成号的每个部分都应该单独考虑。 数字573大于73，因此它是较新的版本。 此外，"2.5" 表示驱动程序的版本号。
