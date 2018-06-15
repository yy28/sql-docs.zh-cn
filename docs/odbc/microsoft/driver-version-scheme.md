---
title: 驱动程序版本方案 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4a6e04da609034fbf0a3d0ba57bc5db2b7b7870
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32900502"
---
# <a name="driver-version-scheme"></a>驱动程序版本方案
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 下表列出所有已发布的版本的 Microsoft ODBC Driver for Oracle。  
  
|驱动程序版本|内部版本号|可用性历史记录|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual c + + 4.2 和 Visual Basic 5.0，Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 和 MDAC 1.5 a|  
|2.0 更新|2.73.7283.01|IIS 4.0|  
|2.0 更新|2.73.7283.03|MDAC 1.5b 和 1.5 c|  
|2.0 更新|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 和 MDAC 2.0|  
|2.5 更新|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 生成 2.00.6235 （版本 1） 适用于 Oracle 的 Microsoft ODBC 驱动程序的第一个版本。 第一个版本的版本之后, 已采用新的命名约定。  
  
 例如，2.73.7283.03 可划分为以下的不同组件：  
  
-   2 = 的版本号。  
  
-   73 = Oracle 服务器为其设计驱动程序的版本。  
  
-   7283.03 = 驱动程序的生成号。  
  
> [!NOTE]  
>  与发行 2.573.2973，请重命名约定导致某些混淆 2.573 是早期版本比 2.73，但应单独考虑每个部分的生成号。 数量 573 大于 73，因此它是较新版本。 此外，"2.5"指示驱动程序的版本号。
