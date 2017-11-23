---
title: "SQLSetConnectAttrForDbcInfo 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f470fe00f7e0d39d2ea474558f21584a75bb42f5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 函数
**一致性**  
 版本引入了： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLSetConnectAttrForDbcInfo**相同**SQLSetConnectAttr**，但它在连接信息令牌，而不是连接句柄上设置的属性。  
  
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
 [输入]要设置的属性。 有效的属性的列表是特定的驱动程序和相同[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 *ValuePtr*  
 [输入]指向要与之关联的值*属性*。 根据值*属性*， *ValuePtr*将成为一个 32 位无符号的整数值，或者将指向以 null 结尾的字符串。 请注意，如果*属性*参数是一个特定于驱动程序的值中的值*ValuePtr*可能是一个带符号的整数。  
  
 *StringLength*  
 [输入]如果*属性*是 ODBC 定义的属性和*ValuePtr*指向字符字符串或二进制缓冲区时，此参数应为的长度 **ValuePtr*。 对于字符串数据，此自变量应包含在字符串中的字节数。  
  
 如果*属性*是 ODBC 定义的属性和*ValuePtr*是一个整数， *StringLength*将被忽略。  
  
 如果*属性*是驱动程序定义的属性，应用程序通过设置指示属性到驱动程序管理器的性质*StringLength*自变量。 *StringLength*可以具有下列值：  
  
-   如果*ValuePtr*然后是指向字符串， *StringLength*是字符串或 sql_nts 以的长度。  
  
-   如果*ValuePtr*为指向二进制缓冲区的指针，则将 SQL_LEN_BINARY_ATTR 结果放置于应用程序 (*长度*) 中的宏*StringLength*。 这会在负值*StringLength*。  
  
-   如果*ValuePtr*然后是指向字符字符串或二进制字符串以外的值的*StringLength*应具有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含固定长度的值，然后*StringLength*为 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，与相应。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 与相同[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，只不过驱动程序管理器将使用**HandleType**的 SQL_HANDLE_DBC_INFO_TOKEN 和**处理**的*hDbcInfoToken*.  
  
## <a name="remarks"></a>注释  
 **SQLSetConnectAttrForDbcInfo**相同**SQLSetConnectAttr**，但它将该属性设置连接信息令牌，而不是连接句柄。 例如，如果**SQLSetConnectAttr**无法识别的属性， **SQLSetConnectAttrForDbcInfo**还应该使 SQL_ERROR 返回该属性。  
  
 每当驱动程序返回 SQL_ERROR 或 SQL_INVALID_HANDLE，驱动程序应忽略此属性来计算池 id。 此外，驱动程序管理器将获取诊断信息从*hDbcInfoToken*，并返回到中的应用程序的 SQL_SUCCESS_WITH_INFO [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). 因此，应用程序可以检索有关无法设置某些属性的原因的详细信息。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h ODBC 驱动程序的开发。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
