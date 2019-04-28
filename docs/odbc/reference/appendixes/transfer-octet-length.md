---
title: 传输八位字节长度 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8f64172685c42a5dde8de9027c8c7e621ddd9f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735063"
---
# <a name="transfer-octet-length"></a>传输八位字节长度
传输八位字节长度的列是最大数据传输到其默认 C 数据类型时返回到应用程序的字节数。 对于字符数据，传输八位字节长度不包括 null 终止字符的空间。 传输八位字节长度的列的可能不同于数据源上存储数据所需的字节数。  
  
 下表中显示为每个 ODBC SQL 数据类型定义的传输八位字节长度。  
  
|SQL 类型标识符|长度|  
|-------------------------|------------|  
|所有字符类型 [a]|定义或列以字节为单位 （适用于变量类型） 最大长度。 这是与描述符字段的 SQL_DESC_OCTET_LENGTH 相同的值。|  
|SQL_DECIMAL<br />SQL_NUMERIC|如果字符设置为 ANSI，保存此数据的字符表示形式所需的字节数和两次此数值的字符集是 UNICODE。 这是因为以字符串形式返回的数据和字符所需的数字、 符号和小数点的数字加两个，最大数目。 例如，定义为 NUMERIC(10,3) 的列的传输长度为 12。|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|如果字符设置为 ANSI，保存此数据的字符表示形式所需的字节数和两次此数值的字符集是 UNICODE，因为默认情况下，此数据类型将返回为字符串。 该字符表示形式包含 20 个字符：数字和符号，已签名，如果为 19 或 20 位数字，如果无符号。 因此，长度为 20。|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|所有二进制类型 [a]|（适用于变量类型） 最大字符数或 （对于固定类型） 保存在定义所需的字节数。|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 （SQL_DATE_STRUCT 或 SQL_TIME_STRUCT 结构的大小）。|  
|SQL_TYPE_TIMESTAMP|16 （SQL_TIMESTAMP_STRUCT 结构的大小）。|  
|所有时间间隔数据类型|34 （间隔结构的大小）。|  
|SQL_GUID|16 （GUID 结构的大小）。|  
  
 [a] 如果驱动程序无法确定变量类型的列或参数长度，它将返回 SQL_NO_TOTAL。
