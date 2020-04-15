---
title: 数据源规范子密钥 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 281377c307f3f3750e87bf5dc988beb7660067af
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300337"
---
# <a name="data-source-specification-subkeys"></a>数据源规范子项
ODBC 数据源子键中列出的每个数据源都有其自己的子密钥。 此子键的名称与 ODBC 数据源子键下的相应值相同。 此子键下的值必须列出驱动程序 DLL，并可以列出数据源的说明。 如果驱动程序支持转换器，则值可以列出默认转换器的名称、默认翻译 DLL 和默认翻译选项。 这些值还可以列出驱动程序连接到数据源所需的其他信息。 例如，驱动程序可能需要服务器名称、数据库名称或架构名称。  
  
 值的格式如下表所示。 仅需要驱动程序值。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|描述|REG_SZ|*描述*|  
|驱动程序|REG_SZ|*驱动程序-DLL 路径*|  
|翻译DLL|REG_SZ|*转换器-DLL 路径*|  
|翻译名称|REG_SZ|*翻译人姓名*|  
|翻译选项|REG_SZ|*翻译选项*|  
|*选择值名称*|*选择价值类型*|*选择价值数据*|  
  
 例如，假设 SQL Server 驱动程序需要服务器名称和 OEM 到 ANSI 转换的标志，并为这些转换定义服务器和 OEMTOANSI 值。 还假设清单数据源使用 Microsoft®代码页转换器在 Windows®拉丁文 1 （1250） 和多语言 （850） 代码页之间进行翻译。 "库存子"项下的值可能如下所示：  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
