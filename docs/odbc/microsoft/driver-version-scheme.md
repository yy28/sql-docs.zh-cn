---
title: 驱动程序版本方案 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303448"
---
# <a name="driver-version-scheme"></a>驱动程序版本方案
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 下表列出了 Oracle 的 Microsoft ODBC 驱动程序的所有已发布版本。  
  
|驱动程序版本|生成号|可用性历史记录|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|视觉C++ 4.2 和视觉基础 5.0，企业版|  
|2.0|2.73.7269|视觉工作室 97 和 MDAC 1.5a|  
|2.0 已更新|2.73.7283.01|IIS 4.0|  
|2.0 已更新|2.73.7283.03|MDAC 1.5b 和 1.5c|  
|2.0 已更新|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|视觉工作室 6.0 和 MDAC 2.0|  
|2.5 更新|2.573.3513|SQL 服务器 7.0<br /><br /> SQL 服务器 6.5 SP5|  
  
 版本 2.00.6235（版本 1）是 Oracle 的 Microsoft ODBC 驱动程序的第一个版本。 在第一个版本发布后，通过了新的命名约定。  
  
 例如，2.73.7283.03 可以分为以下不同的组件：  
  
-   2 = 版本号。  
  
-   73 = 为其设计驱动程序的 Oracle 服务器版本。  
  
-   7283.03 = 驱动程序的生成编号。  
  
> [!NOTE]  
>  对于版本 2.573.2973，命名约定导致一些混淆，即 2.573 是比 2.73 更早版本，但生成编号的每个部分都应单独考虑。 数字 573 大于 73，因此它是一个较新版本。 此外，"2.5"表示驱动程序的版本号。
