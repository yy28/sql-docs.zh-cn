---
title: SQLDataSourceto驱动程序功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSourceToDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSourceToDriver
helpviewer_keywords:
- SQLDataSourceToDriver function [ODBC]
ms.assetid: 0d87fcac-30a0-4303-ad8f-a5b53f4b428d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92df58b76a9a11d0d4ab9821756bff014ecae29a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301187"
---
# <a name="sqldatasourcetodriver-function"></a>SQLDataSourceToDriver 函数
**SQLDataSourceToDriver**支持 ODBC 驱动程序的翻译。 启用 ODBC 的应用程序不调用此功能;应用程序通过**SQLSetConnectAttr**请求转换。 与**SQLSetConnectAttr**中指定的*ConnectHandle*关联的驱动程序调用指定的 DLL 以执行从数据源流向驱动程序的所有数据的转换。 可以在 ODBC 初始化文件中指定默认转换 DLL。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLDataSourceToDriver(  
     UDWORD     fOption,  
     SWORD      fSqlType,  
     PTR        rgbValueIn,  
     SDWORD     cbValueIn,  
     PTR        rgbValueOut,  
     SDWORD     cbValueOutMax,  
     SDWORD *   pcbValueOut,  
     UCHAR *    szErrorMsg,  
     SWORD      cbErrorMsgMax,  
     SWORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>参数  
 *fOption*  
 [输入]选项值。  
  
 *fSqlType*  
 [输入]SQL 数据类型。 此参数告诉驱动程序如何将*rgbValueIn*转换为应用程序可接受的窗体。 有关有效 SQL 数据类型的列表，请参阅附录 D：数据类型中的[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)部分。  
  
 *rgbValuein*  
 [输入]要翻译的值。  
  
 *cbValuein*  
 [输入]*rgbValue 的长度。*  
  
 *rgbValueOut*  
 [输出]翻译结果。  
  
> [!NOTE]  
>  转换 DLL 不为 null 终止此值。  
  
 *cbValueOutMax*  
 [输入]*rgbValueOut 的长度*。  
  
 *pcbValueOut*  
 [输出]可在*rgbValueOut*中返回的字节总数（不包括 null 终止字节）。  
  
 对于字符或二进制数据，如果大于或等于*cbValueOutMax，**则 rgbValueOut*中的数据将被截断为*cbValueOutMax*字节。  
  
 对于所有其他数据类型，将忽略*cbValueOutMax*的值，转换 DLL 假定*rgbValueOut*的大小是使用*fSqlType*指定的 SQL 数据类型的默认 C 数据类型的大小。  
  
 *pcbValueOut*参数可以是空指针。  
  
 *什洛姆斯格*  
 [输出]指向存储的错误消息。 这是一个空字符串，除非翻译失败。  
  
 *cbErrorMsgMax*  
 [输入]*szErrorMsg*的长度。  
  
 *多加错姆斯格*  
 [输出]指向可用在*szErrorMsg*返回的字节总数（不包括空终止字节）的指针。 如果大于或等于*cbErrorMsg，* 则*szErrorMsg*中的数据被截断为*cbErrorMsgMax*减去 null 终止字符。 *pcbErrorMsg*参数可以是空指针。  
  
## <a name="returns"></a>返回  
 如果翻译成功，则为 TRUE，如果翻译失败，则为 FALSE。  
  
## <a name="comments"></a>注释  
 驱动程序调用**SQLDataSourceToDriver**来转换从数据源传递到驱动程序的所有数据（结果集数据、表名、行计数、错误消息等）。 翻译 DLL 可能不会翻译某些数据，具体取决于数据的类型和翻译 DLL 的用途;例如，将字符数据从一个代码页转换为另一个代码页的 DLL 忽略所有数字和二进制数据。  
  
 *fOption*的值设置为*vParam*的值，通过使用SQL_ATTR_TRANSLATE_OPTION属性调用**SQLSetConnectAttr**指定。 它是一个 32 位值，对于给定的翻译 DLL 具有特定的含义。 例如，它可以指定特定的字符集转换。  
  
 如果为*rgbValueIn*和*rgbValueOut*指定了相同的缓冲区，则将就地执行缓冲区中数据的转换。  
  
 虽然*cbValueIn、cbValueOutMax*和*pcbValueOut*是 SDWORD 的类型，但**SQLDataSourceToDriver**不一定支持巨大的指针。 *cbValueIn*  
  
 如果**SQLDataSourceToDriver**返回 FALSE，则可能在转换过程中发生数据截断。 如果*pcbValueOut（* 输出缓冲区中可返回的字节数）大于*cbValueOutMax（* 输出缓冲区的长度），则发生截断。 驱动程序必须确定截断是否可以接受。 如果未发生截断 **，SQLDataSourceToDriver**会返回 FALSE，因为出现另一个错误。 在这两种情况下，在*szErrorMsg*中返回特定的错误消息。  
  
 有关翻译数据的详细信息，请参阅[翻译 DLL](../../../odbc/reference/develop-app/translation-dlls.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|将发送到数据源的数据翻译|[SQLDriverto数据源](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|设置连接属性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
