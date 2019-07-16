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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068566"
---
# <a name="data-source-specification-subkeys"></a>数据源规范子项
在 ODBC 数据源的子项中列出每个数据源都有其自己的子项。 此子项有同名的 ODBC 数据源子项下的相应值。 此子项下的值必须列出驱动程序 DLL，并可能会列出数据源的说明。 如果驱动程序支持的翻译人员，这些值可能会列出默认转换器、 默认转换 DLL 和默认转换选项的名称。 值还可以列出连接到数据源所需的驱动程序的其他信息。 例如，驱动程序可能需要服务器名称、 数据库名称或架构名称。  
  
 值的格式为下表中所示。 仅将驱动程序的值是必需的。  
  
|名称|数据类型|Data|  
|----------|---------------|----------|  
|描述|REG_SZ|*description*|  
|驱动程序|REG_SZ|*driver-DLL-path*|  
|TranslationDLL|REG_SZ|*translator-DLL-path*|  
|TranslationName|REG_SZ|*translator-name*|  
|TranslationOption|REG_SZ|*translation-option*|  
|*opt-value-name*|*opt-value-type*|*opt-value-data*|  
  
 例如，假设 SQL Server 驱动程序到 ANSI 的转换为 OEM 需要服务器名称和一个标志，并且这些定义的服务器和 OEMTOANSI 值。 此外假设库存数据源使用 Microsoft® 代码页转换程序的 Windows® Latin 1 (1250) 和多语言 (850) 代码页之间进行转换。 在清单子项下的值可能按如下所示：  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
