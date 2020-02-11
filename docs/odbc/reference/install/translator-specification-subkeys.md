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
ms.openlocfilehash: ec94f3e02b720617e8f7369b12a916c2bbbe7b16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093798"
---
# <a name="translator-specification-subkeys"></a>转换器规范子项
ODBC 转换器子项中列出的每个转换器都具有自己的子项。 此子项与 ODBC 转换器子项下的相应值具有相同的名称。 此子项下的值列出了转换器和转换器安装程序 Dll 的完整路径以及使用计数。 值的格式如下表中所示。  
  
|名称|数据类型|data|  
|----------|---------------|----------|  
|Translator|REG_SZ|*转换器-DLL-路径*|  
|安装|REG_SZ|*设置-DLL-路径*|  
|UsageCount|REG_DWORD|*计数*|  
  
 有关使用计数的详细信息，请参阅本部分前面的[使用计数](../../../odbc/reference/install/usage-counting.md)。  
  
 应用程序不应设置使用计数。 ODBC 将维护此计数。  
  
 例如，假设 Microsoft 代码页转换器包含一个名为 Mscpxl32 的翻译 DLL，转换器设置函数在同一 DLL 中，并且已安装了三次转换器。 Microsoft 代码页转换器子项下的值如下所示：  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
