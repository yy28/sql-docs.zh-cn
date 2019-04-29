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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e6c76b1a931101fce366cc6d3b20d4aa74de23e5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128044"
---
# <a name="driver-version-scheme"></a>驱动程序版本方案
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 下表列出了适用于 Oracle 的 Microsoft ODBC 驱动程序的所有已发布的版本。  
  
|驱动程序版本|内部版本号|可用性历史记录|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 和 Visual Basic 5.0，企业版|  
|2.0|2.73.7269|Visual Studio 97 和 MDAC 1.5 a|  
|更新 2.0|2.73.7283.01|IIS 4.0|  
|更新 2.0|2.73.7283.03|MDAC 1.5b 和 1.5 c|  
|更新 2.0|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 和 MDAC 2.0|  
|2.5 更新|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 生成 2.00.6235 （版本 1） 是适用于 Oracle 的 Microsoft ODBC 驱动程序的第一个版本。 发布后的第一个版本，采用新的命名约定。  
  
 例如，2.73.7283.03 可以分为以下不同组件：  
  
-   2 = 版本数。  
  
-   73 = Oracle 服务器为其设计驱动程序的版本。  
  
-   7283.03 = 驱动程序的生成号。  
  
> [!NOTE]  
>  与发布 2.573.2973，命名约定具有造成了一些混乱 2.573 更早版本比 2.73，但应单独考虑每个部分的内部版本号。 数字 573 大于 73，因此它是较新版本。 此外，"2.5"指示驱动程序的版本号。
