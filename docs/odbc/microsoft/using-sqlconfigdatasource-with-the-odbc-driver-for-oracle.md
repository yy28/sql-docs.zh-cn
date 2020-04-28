---
title: 将 SQLConfigDatasource 与用于 Oracle 的 ODBC 驱动程序结合使用 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 718e444d63e0d4cf3821c0c03eb851732ed5b4e4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292767"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>配合使用 SQLConfigDatasource 和 Oracle ODBC 驱动程序
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 下表列出了用于 Oracle 的 Microsoft ODBC 驱动程序版本1.0 （Msorcl10）和 Microsoft ODBC Driver for Oracle，版本2.0 （Msorcl32）的有效**SQLConfigDatasource**设置。  
  
> [!NOTE]  
>  Msorcl10 驱动程序（版本1.0）支持除**Server**之外的所有设置。 Msorcl32 驱动程序（版本2.0 及更高版本）支持所有设置。  
  
 某些设置被驱动程序忽略，但被**SQLConfigDatasource**接受。 在 ODBC 连接字符串中包含这些设置是在运行时接受的唯一方法。 当**SQLConfigDatasource**创建数据源时，将不会在注册表中存储被忽略的设置。  
  
 在下表中， */N*表示任意有效的字母数字字符串，最大长度为允许的最大长度。 *最*大长度（最大长度）是设置所允许的最大字符串长度，包括字符串终止符字符。  
  
|设置|最大长度|默认值|有效值|说明|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|最小提取缓冲区大小，最大为65535字节|  
|CatalogCap|2|1|0 或 1|如果为1，则在目录函数中将 nonquoted 标识符转换为大写。|  
|ConnectString|128|""|A/N|连接字符串。 指定包含 Msorcl10 驱动程序的服务器名称所需的方法。|  
|说明|256|""|A/N|说明。|  
|DSN|33|""|A/N|数据源名称。|  
|GuessTheColDef|4|0|A/N|对于没有 Oracle 定义的缩放的列，返回非零值。|  
|NumberFloat|2|""|0 或 1|如果为0，则将 FLOAT 列视为 SQL_FLOAT。 如果为1，则将浮动列视为 SQL_DOUBLE。|  
|PWD|30|""|A/N|Password。|  
|RDOSupport|2|""|0 或 1|允许 RDO 调用 Oracle 过程。|  
|备注|2|0|0 或 1|在目录函数中包含备注。|  
|RowLimit|4|""|0到99|SELECT 语句返回的最大行数。 长度为零的字符串表示未应用限制。|  
|Server (服务器)|128|""|A/N|Oracle 服务器名称。|  
|SynonymColumns|2|1|0 或 1|在 SQLColumns 中包括同义词。|  
|SystemTable|2|""|0 或 1|如果为0，则不显示系统表。 如果为1，则将显示系统表。|  
|TranslationDLL|33|""|A/N|转换 .dll 名称。|  
|TranslationName|33|""|A/N|翻译名称。|  
|TranslationOption|33|""|A/N|转换选项。|  
|TxnCap|2|""|A/N|支持事务。 如果为0，则驱动程序报告它不支持事务。 如果为1，则驱动程序报告它能够执行事务。|  
|UID|30|""|A/N|用户名。|
