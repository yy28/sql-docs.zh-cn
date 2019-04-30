---
title: 转换器规范子项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3c5ad31437cf2639d6b8478d173c7522fa3e9fb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63272941"
---
# <a name="translator-specification-subkeys"></a>转换器规范子项
ODBC 转换器子项中列出每个翻译人员都有其自己的子项。 此子项有同名 ODBC 转换器子项下的相应值。 此子项下的值列出转换器和转换器安装程序 Dll 和使用情况计数的完整的路径。 值的格式为下表中所示。  
  
|“属性”|数据类型|数据|  
|----------|---------------|----------|  
|转换器|REG_SZ|*translator-DLL-path*|  
|安装|REG_SZ|*setup-DLL-path*|  
|UsageCount|REG_DWORD|*计数*|  
  
 有关使用情况计数信息，请参阅[使用情况计数](../../../odbc/reference/install/usage-counting.md)本部分前面。  
  
 应用程序不应设置的使用计数。 ODBC 将保持此计数。  
  
 例如，假设 Microsoft 代码页 Translator 具有名为 Mscpxl32.dll，转换器安装程序函数处于同一个 DLL，DLL 的转换和翻译人员已安装程序三次。 Microsoft 的代码页 Translator 子项下的值可能按如下所示：  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
