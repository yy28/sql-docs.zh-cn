---
title: "数据源规范子项 |Microsoft 文档"
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
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6394b29ff1f76fd0f7edd24a3c239de367c3d58b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="data-source-specification-subkeys"></a>数据源规范子项
在 ODBC 数据源的子项列出每个数据源都有自己的子项。 此子项具有同名的 ODBC 数据源子项下的相应值。 此子项下的值必须列出驱动程序 DLL，并可能会列出数据源的说明。 如果驱动程序支持转换器，值可能会列出默认转换器、 默认转换 DLL 和默认转换选项的名称。 值还可以列出连接到数据源所需的驱动程序的其他信息。 例如，该驱动程序可能需要服务器名称、 数据库名称或架构名称。  
  
 值的格式为下表中所示。 仅将驱动程序值是必需的。  
  
|“属性”|数据类型|data|  
|----------|---------------|----------|  
|Description|REG_SZ|*description*|  
|驱动程序|REG_SZ|*驱动程序的 DLL 的路径*|  
|TranslationDLL|REG_SZ|*转换器的 DLL 的路径*|  
|TranslationName|REG_SZ|*转换器名称*|  
|TranslationOption|REG_SZ|*翻译选项*|  
|*选择值名称*|*选择值类型*|*选择值数据*|  
  
 例如，假设 SQL Server 驱动程序要求的服务器名称和一个标志针对 OEM ANSI 转换，并且这些定义的服务器和 OEMTOANSI 值。 同时假定清单数据源使用 Microsoft® 代码页转换器 Windows® 拉丁文 1 (1250) 和多语言 (850) 代码页之间进行转换。 清单子项下的值可能如下所示：  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
