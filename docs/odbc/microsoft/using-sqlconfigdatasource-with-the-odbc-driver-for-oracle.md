---
title: 使用 Oracle ODBC 驱动程序随 SQLConfigDatasource |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b412d422251cfb29f4e036ac3d7db2d3e528c5e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>使用 Oracle ODBC 驱动程序随 SQLConfigDatasource
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 下表列出有效**SQLConfigDatasource** Microsoft ODBC Driver for Oracle，版本 1.0 (Msorcl10.dll) 和 Microsoft ODBC Driver for Oracle，版本 2.0 (Msorcl32.dll) 设置。  
  
> [!NOTE]  
>  Msorcl10.dll 驱动程序 （1.0 版） 支持所有设置除外**服务器**。 Msorcl32.dll 驱动程序 （版本 2.0 和更高版本） 支持的所有设置。  
  
 某些设置由驱动程序将被忽略，但接受**SQLConfigDatasource**。 在 ODBC 连接字符串中包含这些设置是他们将在运行时接受的唯一方法。 忽略的设置不会存储在注册表中时**SQLConfigDatasource**创建数据源。  
  
 在以下表中， *A/N*意味着任何有效的字母数字字符串，直到最大允许长度。 *最大 Len* （最大长度） 是接受的设置，包括字符串终止符字符的最大允许字符串长度。  
  
|设置|最大长度|默认值|有效值|Description|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|最小提取缓冲区大小最多 65535 字节|  
|CatalogCap|2|1|0 或 1|如果为 1，nonquoted 的标识符将转换为大写形式在目录中的函数。|  
|ConnectString|128|""|A/N|连接字符串。 所需的指定服务器名称使用 Msorcl10.dll 驱动程序的方法。|  
|Description|256|""|A/N|说明。|  
|DSN|33|""|A/N|数据源名称。|  
|GuessTheColDef|4|0|A/N|返回列缺少 Oracle 定义小数位数为非零值。|  
|NumberFloat|2|""|0 或 1|如果为 0，FLOAT 列视为 SQL_FLOAT。 如果为 1，FLOAT 列视为 SQL_DOUBLE。|  
|PWD|30|""|A/N|密码。|  
|RDOSupport|2|""|0 或 1|允许 RDO 调用 Oracle 过程。|  
|注释|2|0|0 或 1|包含目录函数中的备注。|  
|RowLimit|4|""|0 到 99|由 SELECT 语句返回的行的最大数量。 长度为零的字符串表示应用没有限制。|  
|Server|128|""|A/N|Oracle 服务器名称。|  
|SynonymColumns|2|1|0 或 1|SQLColumns 中包括的同义词。|  
|SystemTable|2|""|0 或 1|如果为 0，则不会显示系统表。 如果为 1，则将显示系统表。|  
|TranslationDLL|33|""|A/N|转换.dll 的名称。|  
|TranslationName|33|""|A/N|转换的名称。|  
|TranslationOption|33|""|A/N|转换选项。|  
|TxnCap|2|""|A/N|事务支持。 如果为 0，驱动程序报告称它不支持事务。 如果为 1，该驱动程序报告它能够执行事务。|  
|UID|30|""|A/N|用户名称。|
