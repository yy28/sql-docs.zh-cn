---
title: SQLDriverToDataSource 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverToDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverToDataSource
helpviewer_keywords:
- SQLDriverToDataSource function [ODBC]
ms.assetid: 0de28eb5-8aa9-43e4-a87f-7dbcafe800dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f5450bbabb43b1f5cbc8c0fd7cb1a83da3a8bc7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061438"
---
# <a name="sqldrivertodatasource-function"></a>SQLDriverToDataSource 函数
**SQLDriverToDataSource**的 ODBC 驱动程序支持翻译。 不支持 ODBC 的应用程序; 通过调用此函数应用程序请求通过翻译**SQLSetConnectAttr**。 与关联的驱动程序*ConnectionHandle*中指定**SQLSetConnectAttr**调用指定的 DLL 执行从驱动程序流动到数据源的所有数据的转换。 可以在 ODBC 初始化文件中指定默认转换 DLL。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLDriverToDataSource(  
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
 [输入]ODBC SQL 数据类型。 此参数指示驱动程序如何将转换*rgbValueIn*到数据源可接受一个窗体。 有关有效的 SQL 数据类型的列表，请参阅[SQL 数据类型](../../../odbc/reference/appendixes/sql-data-types.md)。  
  
 *rgbValueIn*  
 [输入]要转换的值。  
  
 *cbValueIn*  
 [输入]长度*rgbValueIn*。  
  
 *rgbValueOut*  
 [输出]转换的结果。  
  
> [!NOTE]  
>  转换 DLL 不会为 null 的终止此值。  
  
 *cbValueOutMax*  
 [输入]长度*rgbValueOut*。  
  
 *pcbValueOut*  
 [输出]的总字节数 （不包括 null 终止字节） 可用于在中返回*rgbValueOut*。  
  
 为字符或二进制数据，如果这是大于或等于*cbValueOutMax*中的数据*rgbValueOut*将被截断为*cbValueOutMax*字节。  
  
 对于所有其他数据类型，值*cbValueOutMax*将被忽略，并转换 DLL 假定的大小*rgbValueOut* 与指定的SQL数据类型的默认C数据类型的大小*fSqlType*。  
  
 *PcbValueOut*参数可以是 null 指针。  
  
 *szErrorMsg*  
 [输出]一个指针，指向存储为一条错误消息。 除非转换失败，这是一个空字符串。  
  
 *cbErrorMsgMax*  
 [输入]长度*szErrorMsg*。  
  
 *pcbErrorMsg*  
 [输出]指向的总字节数 （不包括 null 终止字节） 可用于在中返回*szErrorMsg*。 如果这是大于或等于*cbErrorMsg*中的数据*szErrorMsg*将被截断为*cbErrorMsgMax*减号 null 终止字符。 *PcbErrorMsg*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 如果转换成功，则返回 FALSE 如果转换失败，则为 TRUE。  
  
## <a name="comments"></a>注释  
 驱动程序调用**SQLDriverToDataSource**转换所有数据 （SQL 语句、 参数等） 将驱动程序传递到数据源。 转换 DLL 可能无法保证某些数据，具体取决于数据的类型和用途的转换 DLL。 例如，转换字符数据从一个代码页到另一个 DLL 将忽略所有数值和二进制数据。  
  
 值*fOption*设置为值*vParam*指定通过调用**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 属性。 它是具有预定义的给定转换 DLL 的 32 位值。 例如，它可以指定特定字符设置翻译。  
  
 如果为指定同一缓冲区*rgbValueIn*并*rgbValueOut*，缓冲区中的数据转换将就地执行。  
  
 尽管*cbValueIn*， *cbValueOutMax*，并*pcbValueOut*属于类型 SDWORD， **SQLDriverToDataSource**不一定不会支持大量的指针。  
  
 如果**SQLDriverToDataSource**返回 FALSE，在转换期间可能发生数据截断。 如果*pcbValueOut* （可在输出缓冲区中返回的字节数） 大于*cbValueOutMax* （输出缓冲区的长度），则发生截断。 该驱动程序必须确定截断可接受。 如果不发生截断，一样**SQLDriverToDataSource**由于另一个错误返回 FALSE。 在任一情况下，特定的错误消息中返回*szErrorMsg*。  
  
 有关将数据转换的详细信息，请参阅[转换 Dll](../../../odbc/reference/develop-app/translation-dlls.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|从数据源将数据转换返回|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|将连接属性设置|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
