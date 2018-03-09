---
title: "转换器规范子项 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 86ba311eb458c1128a611b6d1cc2ed1c71329d3f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="translator-specification-subkeys"></a>转换器规范子项
ODBC 转换器子项中列出每个翻译人员都有自己的子项。 此子项具有相同名称，为 ODBC 转换器子项下相应的值。 此子项下的值列表转换器和转换器设置 Dll 和使用情况计数的完整的路径。 值的格式为下表中所示。  
  
|“属性”|数据类型|data|  
|----------|---------------|----------|  
|转换器|REG_SZ|*转换器的 DLL 的路径*|  
|安装|REG_SZ|*安装程序的 DLL 的路径*|  
|UsageCount|REG_DWORD|*计数*|  
  
 有关使用情况计数的信息，请参阅[使用情况计数](../../../odbc/reference/install/usage-counting.md)本部分前面的。  
  
 应用程序不应设置的使用计数。 ODBC 将维护此计数。  
  
 例如，假设 Microsoft 代码页转换器的转换是 DLL 名为 Mscpxl32.dll，转换器设置功能处于同一个 DLL，并且初始屏幕转换器已安装程序三次。 Microsoft 代码页转换器子项下的值可能如下所示：  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
