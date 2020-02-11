---
title: 数据源规范子项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fae642b46b4c652583622ec4832b3217d0b1681c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068566"
---
# <a name="data-source-specification-subkeys"></a>数据源规范子项
ODBC 数据源子项中列出的每个数据源都有自己的子项。 此子项与 ODBC 数据源子项下的相应值具有相同的名称。 此子项下的值必须列出驱动程序 DLL，并且可能会列出数据源的说明。 如果驱动程序支持转换器，这些值可能会列出默认转换器、默认翻译 DLL 和默认转换选项的名称。 值还可能列出驱动程序连接到数据源所需的其他信息。 例如，驱动程序可能需要服务器名称、数据库名称或架构名称。  
  
 值的格式如下表中所示。 只有驱动程序值是必需的。  
  
|名称|数据类型|data|  
|----------|---------------|----------|  
|说明|REG_SZ|*2008*|  
|驱动程序|REG_SZ|*驱动程序-DLL-路径*|  
|TranslationDLL|REG_SZ|*转换器-DLL-路径*|  
|TranslationName|REG_SZ|*转换器-名称*|  
|TranslationOption|REG_SZ|*转换-选项*|  
|*选择值名称*|*opt-值类型*|*选择值-数据*|  
  
 例如，假设 SQL Server 驱动程序需要使用服务器名称和标记进行 OEM 到 ANSI 的转换，并为这些转换定义服务器值和 OEMTOANSI 值。 假设清单数据源使用 Microsoft®代码页转换器来转换 Windows®拉丁语1（1250）和多语言（850）代码页。 清单子项下的值可能如下所示：  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
