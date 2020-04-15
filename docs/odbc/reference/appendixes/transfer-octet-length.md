---
title: 传输八进制长度 |微软文档
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4204b47816747506a5672241eeeef736eca54856
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302808"
---
# <a name="transfer-octet-length"></a>传输八位字节长度
列的传输八字形长度是将数据传输到其默认 C 数据类型时返回给应用程序的最大字节数。 对于字符数据，传输八字形长度不包括空终止字符的空间。 列的传输八进制长度可能与将数据存储在数据源上所需的字节数不同。  
  
 为每种 ODBC SQL 数据类型定义的传输八进制长度显示在下表中。  
  
|SQL 类型标识符|长度|  
|-------------------------|------------|  
|所有字符类型[a]|以字节为单位的列的已定义或最大长度（对于变量类型）。 这与描述符字段SQL_DESC_OCTET_LENGTH的值相同。|  
|SQL_DECIMAL<br />SQL_NUMERIC|如果字符集为 ANSI，则保存此数据的字符表示形式所需的字节数;如果字符集为 UNICODE，则此数字为两倍。 这是数字加上两个的最大数字数，因为数据作为字符串返回，数字、符号和小数点需要字符。 例如，定义为数字（10，3）的列的传输长度为 12。|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT| 8 |  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|所有二进制类型[a]|保存定义的（对于固定类型）或最大（对于变量类型）字符数所需的字节数。|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6（SQL_DATE_STRUCT或SQL_TIME_STRUCT结构的大小）。|  
|SQL_TYPE_TIMESTAMP|16 （SQL_TIMESTAMP_STRUCT结构的大小）。|  
|所有间隔数据类型|34 （间隔结构的大小）。|  
|SQL_GUID|16 （GUID 结构的大小）。|  
| &nbsp; | &nbsp; |

 [a] 如果驱动程序无法确定变量类型的列或参数长度，则返回SQL_NO_TOTAL。
