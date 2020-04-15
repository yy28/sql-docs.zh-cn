---
title: SQLSetConnecttfordbcinfo 功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f43a0fc6cd02fe566579a543667f9a4c4c1a108
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301884"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 函数
**一致性**  
 版本介绍： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLSetConnectTrForDbcInfo**与**SQLSetConnectAttr**相同，但它在连接信息令牌上而不是在连接句柄上设置属性。  
  
## <a name="syntax"></a>语法  
  
```cpp
  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>参数  
 *hDbcInfoToken*  
 [输入]令牌句柄。  
  
 *特性*  
 [输入]要设置的属性。 有效属性的列表特定于驱动程序，与[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同。  
  
 *ValuePtr*  
 [输入]指向要与*属性*关联的值的指针。 根据*属性*的值 *，ValuePtr*将是一个 32 位未符号整数值，或将指向 null 端接的字符串。 请注意，如果*属性*参数是特定于驱动程序的值 *，ValuePtr*中的值可能是已签名的整数。  
  
 *字符串长度*  
 [输入]如果*属性*是 ODBC 定义的属性 *，ValuePtr*指向字符串或二进制缓冲区，则此参数应为 **ValuePtr*的长度。 对于字符串数据，此参数应包含字符串中的字节数。  
  
 如果*属性*是 ODBC 定义的属性 *，ValuePtr*是整数，则忽略*字符串长度*。  
  
 如果*属性*是驱动程序定义的属性，则应用程序通过设置*StringLength*参数指示该属性对驱动程序管理器的性质。 *字符串长度*可以具有以下值：  
  
-   如果*ValuePtr*是指向字符串的指针，则*StringLength*是字符串的长度或SQL_NTS。  
  
-   如果*ValuePtr*是指向二进制缓冲区的指针，则应用程序将SQL_LEN_BINARY_ATTR（*长度*）宏的结果放在*StringLength 中*。 这将在*字符串长度*中放置负值。  
  
-   如果*ValuePtr*是指向字符串或二进制字符串以外的值的指针，则*StringLength*应具有该值SQL_IS_POINTER。  
  
-   如果*ValuePtr*包含固定长度值，则*StringLength*会根据需要SQL_IS_INTEGER或SQL_IS_UINTEGER。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 与[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)相同 ，只不过驱动程序管理器将使用SQL_HANDLE_DBC_INFO_TOKEN的**句柄类型**和*hDbcInfoToken*的**句柄**。  
  
## <a name="remarks"></a>备注  
 **SQLSetConnectTrForDbcInfo**与**SQLSetConnectAttr**相同，但它在连接信息令牌上设置属性，而不是在连接句柄上设置属性。 例如，如果**SQLSetConnectAttr**无法识别属性，**则 SQLSetConnectAttrForDbcInfo**也应返回该属性SQL_ERROR。  
  
 每当驱动程序返回SQL_ERROR或SQL_INVALID_HANDLE时，驱动程序应忽略此属性以计算池 ID。 此外，驱动程序管理器将从*hDbcInfoToken*获取诊断信息，并将SQL_SUCCESS_WITH_INFO返回到[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中的应用程序。 因此，应用程序可以检索有关无法设置某些属性的原因的详细信息。  
  
 应用程序不应直接调用此功能。 支持驱动程序感知连接池的 ODBC 驱动程序必须实现此功能。  
  
 包括用于 ODBC 驱动程序开发的 sqlspi.h。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
