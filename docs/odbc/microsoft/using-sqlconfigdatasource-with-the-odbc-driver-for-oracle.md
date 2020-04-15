---
title: 将 SQLConfigDatasource 与 Oracle 的 ODBC 驱动程序结合使用 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292767"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>配合使用 SQLConfigDatasource 和 Oracle ODBC 驱动程序
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 下表列出了适用于 Oracle 的 Microsoft ODBC 驱动程序、版本 1.0（Msorcl10.dll） 和 Oracle 的 Microsoft ODBC 驱动程序（2.0 版（Msorcl32.dll）的有效**SQLConfigDatasource**设置。  
  
> [!NOTE]  
>  Msorcl10.dll 驱动程序（版本 1.0）支持**除服务器**之外的所有设置。 Msorcl32.dll 驱动程序（版本 2.0 及以上）支持所有设置。  
  
 某些设置被驱动程序忽略，但**SQLConfigDatasource**接受。 在 ODBC 连接字符串中包含这些设置是运行时接受这些设置的唯一方法。 **当 SQLConfigDatasource**创建数据源时，忽略的设置将不会存储在注册表中。  
  
 在下表中 *，A/N*表示任何有效的字母数字字符串，最长可达允许长度。 *最大 Len（* 最大长度）是设置接受的最大允许字符串长度，包括字符串终结器字符。  
  
|设置|马克斯·伦|默认值|有效值|描述|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|最小提取缓冲区大小高达 65535 字节|  
|目录帽|2|1|0 或 1|如果为 1，则非引号标识符将在目录函数中转换为大写。|  
|连接字符串|128|""|A/N|连接字符串。 使用 Msorcl10.dll 驱动程序指定服务器名称的必需方法。|  
|描述|256|""|A/N|说明。|  
|DSN|33|""|A/N|数据源名称。|  
|猜谜|4|0|A/N|为没有 Oracle 定义的比例的列返回非零值。|  
|数量浮动|2|""|0 或 1|如果为 0，则 FLOAT 列将被视为SQL_FLOAT。 如果为 1，则 FLOAT 列将被视为SQL_DOUBLE。|  
|PWD|30|""|A/N|Password。|  
|RDO支持|2|""|0 或 1|允许 RDO 调用 Oracle 过程。|  
|备注|2|0|0 或 1|在目录函数中包括注释。|  
|行限制|4|""|0 到 99|SELECT 语句返回的最大行数。 零长度字符串表示不应用任何限制。|  
|服务器|128|""|A/N|Oracle 服务器名称。|  
|同义词列|2|1|0 或 1|在 SQL 栏中包括 SYNONYM。|  
|系统表|2|""|0 或 1|如果为 0，则不会显示系统表。 如果为 1，则将显示系统表。|  
|翻译DLL|33|""|A/N|翻译 .dll 名称。|  
|翻译名称|33|""|A/N|翻译名称。|  
|翻译选项|33|""|A/N|翻译选项。|  
|TxnCap|2|""|A/N|事务能力。 如果为 0，驱动程序将报告它不支持事务。 如果为 1，则驱动程序报告它能够执行事务。|  
|UID|30|""|A/N|用户名。|
