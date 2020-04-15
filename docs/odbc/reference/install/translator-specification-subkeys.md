---
title: 转换器规格子键 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad21943c5313edcb09aba88d45ea21132aa9757f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296037"
---
# <a name="translator-specification-subkeys"></a>转换器规范子项
ODBC 翻译人员子键中列出的每个转换器都有其自己的子密钥。 此子键的名称与 ODBC 翻译器子键下的相应值相同。 此子键下的值列出了转换器和转换器设置 DLL 的完整路径和使用计数。 值的格式如下表所示。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|转换器|REG_SZ|*转换器-DLL 路径*|  
|设置|REG_SZ|*设置-DLL路径*|  
|使用情况计数|REG_DWORD|*count*|  
  
 有关使用情况计数的信息，请参阅本节前面[先查看使用情况计数](../../../odbc/reference/install/usage-counting.md)。  
  
 应用程序不应设置使用计数。 ODBC 将保留此计数。  
  
 例如，假设 Microsoft 代码页转换器具有名为 Mscpxl32.dll 的翻译 DLL，其中译员的设置功能位于同一 DLL 中，并且译员已安装三次。 Microsoft 代码页翻译子键下的值可能如下所示：  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
