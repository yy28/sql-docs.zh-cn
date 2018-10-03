---
title: SQLSetConnectAttrForDbcInfo 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 798f986adfeda95ef091161458d94c2ccc33b2e3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818475"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 函数
**符合性**  
 版本引入了： ODBC 3.81 标准符合性： ODBC  
  
 **摘要**  
 **SQLSetConnectAttrForDbcInfo**等同于**SQLSetConnectAttr**，但它的连接信息令牌而不是连接句柄上设置的属性。  
  
## <a name="syntax"></a>语法  
  
```  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>参数  
 *hDbcInfoToken*  
 [输入]标记句柄。  
  
 *Attribute*  
 [输入]若要设置的属性。 有效的属性列表是驱动程序特定和的相同[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 *ValuePtr*  
 [输入]指向要与之关联的值*属性*。 具体取决于值*特性*， *ValuePtr*值将为 32 位无符号的整数值或将指向以 null 结尾的字符串。 请注意，如果*特性*自变量是特定于驱动程序的值中的值*ValuePtr*可能是一个有符号的整数。  
  
 *StringLength*  
 [输入]如果*特性*是一个 ODBC 定义的属性和*ValuePtr*指向字符字符串或二进制缓冲区中，此参数应为的长度 **ValuePtr*。 对于字符串数据，此参数应包含在字符串中的字节数。  
  
 如果*特性*是一个 ODBC 定义的属性和*ValuePtr*是一个整数*StringLength*将被忽略。  
  
 如果*特性*是一个驱动程序定义的属性，该应用程序通过设置指示特性的驱动程序管理器的性质*StringLength*参数。 *StringLength*可以具有以下值：  
  
-   如果*ValuePtr*是一个指向一个字符串，然后*StringLength*是 sql_nts; 的字符串的长度。  
  
-   如果*ValuePtr*是一个指向二进制缓冲区，则 SQL_LEN_BINARY_ATTR 将结果放置于该应用程序 (*长度*) 中的宏*StringLength*。 这会在负值*StringLength*。  
  
-   如果*ValuePtr*指向的字符串或二进制字符串以外的值，即*StringLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含一个固定长度值，则*StringLength*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，根据需要。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 与相同[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，只不过驱动程序管理器将使用**HandleType** SQL_HANDLE_DBC_INFO_TOKEN 的和一个**处理**的*hDbcInfoToken*.  
  
## <a name="remarks"></a>备注  
 **SQLSetConnectAttrForDbcInfo**等同于**SQLSetConnectAttr**，但它的属性上的连接信息令牌，而不是在上设置连接句柄。 例如，如果**SQLSetConnectAttr**不能识别特性**SQLSetConnectAttrForDbcInfo**还会为该属性返回 SQL_ERROR。  
  
 该驱动程序时驱动程序将返回 SQL_ERROR 或 SQL_INVALID_HANDLE，应忽略此属性来计算池 id。 此外，驱动程序管理器将获取的诊断信息*hDbcInfoToken*，并返回 SQL_SUCCESS_WITH_INFO 到中的应用程序[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). 因此，应用程序可以检索有关为什么无法设置某些属性的详细信息。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h 的 ODBC 驱动程序开发。  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
