---
title: 聚合函数、 CALC 函数和 NEW 关键字 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0a72cf80f9fee9c887e7805f3a2a5bd542d7f47c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702423"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>聚合函数、CALC 函数和 NEW 关键字
数据整理支持以下函数。 分配给包含的列的一章来操作的名称是*章别名*。  
  
 可以是完全限定，包含通向章包含每个章节列名称的一章别名*列名，* 各项之间由句点。 例如，如果父一章，chap1，包含子章节，chap2，具有一个 amount 列，amt 设置，则限定的名称将为 chap1.chap2.amt。  
  
|聚合函数|Description|  
|-------------------------|-----------------|  
|SUM (*章别名*。*列名称*)|计算指定列中的所有值的总和。|  
|AVG (*章别名*。*列名称*)|计算指定列中的所有值的平均值。|  
|最大值 (*章别名*。*列名称*)|计算指定列中的最大值。|  
|最小值 (*章别名*。*列名称*)|计算指定列中的最小值。|  
|计数 (*章别名*[。*列名称*])|对指定的别名中的行数进行计数。 如果指定的列，该列为其为非 Null 的唯一行包含在计数中。|  
|STDEV (*章别名*。*列名称*)|计算指定列中的标准偏差。|  
|任何 (*章别名*。*列名称*)|指定列的值。 仅当列的值是相同的一章中的所有行时，任何具有可预测的值。<br /><br /> **请注意**列不包含所有一章中的行的相同值，如果形状命令任意返回值的任何函数的值之一。|  
  
|计算的表达式|Description|  
|---------------------------|-----------------|  
|CALC(*expression*)|计算的任意表达式，但只能在的行上**记录集**包含 CALC 函数。 任何表达式中使用这些[Visual Basic for Applications (VBA) 函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)允许。|  
  
|新的关键字|Description|  
|-----------------|-----------------|  
|NEW *field-type* [(*width* &#124; *scale* &#124; *precision* &#124; *error* [, *scale* &#124; *error*])]|将添加到指定的类型的空列**记录集**。|  
  
 *字段类型*传递使用 NEW 关键字可以是任何以下数据类型。  
  
|OLE DB 数据类型|ADO 数据类型 equivalent(s)|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|adBoolean|  
|DBTYPE_DECIMAL|adDecimal|  
|DBTYPE_UI1|adUnsignedTinyInt|  
|DBTYPE_I1|adTinyInt|  
|DBTYPE_UI2|adUnsignedSmallInt|  
|DBTYPE_UI4|adUnsignedInt|  
|DBTYPE_I8|adBigInt|  
|DBTYPE_UI8|adUnsignedBigInt|  
|DBTYPE_GUID|adGuid|  
|DBTYPE_BYTES|adBinary, AdVarBinary, adLongVarBinary|  
|DBTYPE_STR|每，以便您可以排除 adLongVarChar|  
|DBTYPE_WSTR|adWChar，adVarWChar adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 （在 OLE DB DBTYPE_DECIMAL，或在 ADO 中，adDecimal） 十进制类型的新字段时，必须指定的精度和小数位数的值。  
  
## <a name="see-also"></a>请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
