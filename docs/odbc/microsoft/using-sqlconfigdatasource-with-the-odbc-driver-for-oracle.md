---
title: 用于 Oracle 的 ODBC 驱动程序配合使用 SQLConfigDatasource |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9edd9ae15e66a39abd84a8a6d8e50a83ed4a39ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259339"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>配合使用 SQLConfigDatasource 和 Oracle ODBC 驱动程序
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 下表列出了有效**SQLConfigDatasource** Microsoft ODBC Driver for Oracle，版本 1.0 (Msorcl10.dll) 和 Microsoft ODBC Driver for Oracle，版本 2.0 (Msorcl32.dll) 的设置。  
  
> [!NOTE]  
>  Msorcl10.dll 驱动程序 （版本 1.0） 支持所有的设置除外**Server**。 Msorcl32.dll 驱动程序 （版本 2.0 及更高版本） 支持的所有设置。  
  
 某些设置由驱动程序忽略但被接受**SQLConfigDatasource**。 ODBC 连接字符串中包含这些设置是会在运行时接受它们的唯一方法。 已忽略的设置不会存储在注册表中时**SQLConfigDatasource**创建数据源。  
  
 下表中*A/N*意味着任何有效的字母数字字符串最多的最大长度。 *最大 Len* （最大长度） 是接受的设置，包括字符串终止符字符的最大允许字符串长度。  
  
|设置|最大长度|默认值|有效值|Description|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|最小的提取缓冲区大小最多 65535 字节|  
|CatalogCap|2|1|0 或 1|如果为 1，nonquoted 的标识符将转换为大写的目录中的函数。|  
|ConnectString|128|""|A/N|连接字符串。 指定服务器名称使用 Msorcl10.dll 驱动程序的所需的方法。|  
|Description|256|""|A/N|说明。|  
|DSN|33|""|A/N|数据源名称。|  
|GuessTheColDef|4|0|A/N|返回没有 Oracle 定义的小数位的列的非零值。|  
|NumberFloat|2|""|0 或 1|如果为 0，FLOAT 列被视为 SQL_FLOAT。 如果为 1，FLOAT 列被视为 SQL_DOUBLE。|  
|PWD|30|""|A/N|密码。|  
|RDOSupport|2|""|0 或 1|允许 RDO 调用 Oracle 过程。|  
|备注|2|0|0 或 1|包括目录中的备注。|  
|RowLimit|4|""|0 到 99|由 SELECT 语句返回的行的最大数目。 长度为零的字符串表示应用没有限制。|  
|“服务器”|128|""|A/N|Oracle 服务器名称。|  
|SynonymColumns|2|1|0 或 1|SQLColumns 中包括同义词。|  
|SystemTable|2|""|0 或 1|如果为 0，则不会显示系统表。 如果为 1，将显示系统表。|  
|TranslationDLL|33|""|A/N|转换的.dll 名称。|  
|TranslationName|33|""|A/N|转换的名称。|  
|TranslationOption|33|""|A/N|转换选项。|  
|TxnCap|2|""|A/N|事务支持。 如果为 0，驱动程序报告不支持事务。 如果为 1，驱动程序报告是能够执行的事务。|  
|UID|30|""|A/N|用户名称。|
