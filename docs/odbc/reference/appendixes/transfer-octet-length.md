---
title: 传输八位字节长度 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 157dbea8954dd7823888360c7d9cf74d9c8db74d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909753"
---
# <a name="transfer-octet-length"></a>传输八位字节长度
传输八位字节长度的列是最大数据传输到其默认 C 数据类型时返回到应用程序的字节数。 对于字符数据，传输八位字节长度不包括 null 终止字符的空间。 传输八位字节长度的列可能不同于数据源上存储数据所需的字节数。  
  
 下表中显示为每个 ODBC SQL 数据类型定义的传输八位字节长度。  
  
|SQL 类型标识符|长度|  
|-------------------------|------------|  
|所有字符类型 [a]|定义或以字节为单位的列的最大值 （为变量类型） 长度。 这是描述符字段 SQL_DESC_OCTET_LENGTH 相同的值。|  
|SQL_DECIMAL<br />SQL_NUMERIC|保存此数据的字符表示的字符集为 ANSI，如果所需的字节数和两次此号如果字符集采用 unicode 编码。 这是最大数数字加上两个，因为字符串形式返回的数据和有关每个数字、 符号和小数点需要个字符。 例如，定义为 NUMERIC(10,3) 的列的传输长度为 12。|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|保存此数据的字符表示的字符集为 ANSI，如果所需的字节数和两次此号如果字符集采用 unicode 编码，因为默认情况下，此数据类型将返回字符串形式。 该字符表示形式包含 20 个字符： 19 的数字和一个符号，如果已签名，或者 20 的数字，如果未签名。 因此，长度为 20。|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|所有二进制类型 [a]|（对于变量类型） 最大字符数或 （对于固定类型） 保存定义所需的字节数。|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 （SQL_DATE_STRUCT 或 SQL_TIME_STRUCT 结构的大小）。|  
|SQL_TYPE_TIMESTAMP|16 （SQL_TIMESTAMP_STRUCT 结构的大小）。|  
|所有 interval 数据类型|34 （间隔结构的大小）。|  
|SQL_GUID|16 （GUID 结构的大小）。|  
  
 [a] 如果驱动程序无法确定变量类型的列或参数长度，它将返回 SQL_NO_TOTAL。
