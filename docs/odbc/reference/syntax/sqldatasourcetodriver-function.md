---
title: SQLDataSourceToDriver 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d09d649bc53a08ff7389413882bb338d9713ffc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqldatasourcetodriver-function"></a>SQLDataSourceToDriver 函数
**SQLDataSourceToDriver** supportstranslations ODBC 驱动程序。 不支持 ODBC 的应用程序; 调用此函数应用程序请求通过翻译**SQLSetConnectAttr**。 与关联的驱动程序*ConnectionHandle*中指定**SQLSetConnectAttr**调用指定的 DLL，若要执行的所有数据从数据源流向驱动程序的翻译。 ODBC 初始化文件中，可以指定默认转换 DLL。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 [输入]SQL 数据类型。 此参数指示驱动程序如何将转换*rgbValueIn*到窗体应用程序可接受。 有关有效的 SQL 数据类型的列表，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)附录 d： 数据类型中的部分。  
  
 *rgbValueIn*  
 [输入]要转换的值。  
  
 *cbValueIn*  
 [输入]长度*rgbValueIn*。  
  
 *rgbValueOut*  
 [输出]转换的结果。  
  
> [!NOTE]  
>  转换 DLL 不 null-终止此值。  
  
 *cbValueOutMax*  
 [输入]长度*rgbValueOut*。  
  
 *pcbValueOut*  
 [输出]总 （不包括 null 终止字节） 的字节数可用于返回在*rgbValueOut*。  
  
 字符或二进制数据，如果这是大于或等于*cbValueOutMax*中的数据*rgbValueOut*截断为*cbValueOutMax*字节。  
  
 对于所有其他数据类型的值*cbValueOutMax*将被忽略并转换 DLL 假定的大小*rgbValueOut*是与指定的SQL数据类型的默认C数据类型的大小*fSqlType*。  
  
 *PcbValueOut*参数可以是 null 指针。  
  
 *szErrorMsg*  
 [输出]到存储中获得一条错误消息的指针。 除非的转换失败，这是一个空字符串。  
  
 *cbErrorMsgMax*  
 [输入]长度*szErrorMsg*。  
  
 *pcbErrorMsg*  
 [输出]（不包括 null 终止字节） 的字节总数的指针可用于返回在*szErrorMsg*。 如果这是大于或等于*cbErrorMsg*中的数据*szErrorMsg*截断为*cbErrorMsgMax*减去的 null 终止字符。 *PcbErrorMsg*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 如果转换成功，则返回 FALSE 如果转换失败，则为 TRUE。  
  
## <a name="comments"></a>注释  
 驱动程序调用**SQLDataSourceToDriver**转换 alldata （结果集数据、 表名称、 行计数、 错误消息，等等） 的数据传递，源到驱动程序。 转换 DLL，则会将一些数据，具体取决于数据的类型和用途的转换 DLL; 可能不转换例如，一个 DLL，它将转换字符数据从一个代码页复制到另一个将忽略所有的数字和二进制数据。  
  
 值*fOption*设置的值为*vParam*指定通过调用**SQLSetConnectAttr**具有 SQL_ATTR_TRANSLATE_OPTION 属性。 它是具有特定含义为给定翻译 DLL 的 32 位值。 例如，它可以指定某些字符集转译。  
  
 如果对同一缓冲区指定为*rgbValueIn*和*rgbValueOut*，缓冲区中数据的转换将就地执行。  
  
 尽管*cbValueIn*， *cbValueOutMax*，和*pcbValueOut*属于类型 SDWORD， **SQLDataSourceToDriver**不一定不支持巨大的指针。  
  
 如果**SQLDataSourceToDriver**返回 FALSE，转换期间可能发生数据截断。 如果*pcbValueOut* （可用于返回中输出缓冲区的字节数） 大于*cbValueOutMax* （输出缓冲区的长度），则发生截断。 该驱动程序必须确定是否可接受截断。 如果未出现截断， **SQLDataSourceToDriver**由于另一个错误返回 FALSE。 在任一情况下，特定的错误消息中返回*szErrorMsg*。  
  
 有关将数据转换的详细信息，请参阅[转换 Dll](../../../odbc/reference/develop-app/translation-dlls.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|将发送到数据源的数据转换|[SQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|将连接属性设置|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
