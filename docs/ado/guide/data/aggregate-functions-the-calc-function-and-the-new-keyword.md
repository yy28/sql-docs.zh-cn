---
title: 聚合函数、 CALC 函数中和 NEW 关键字 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ead07efd4c56b01b50f78c0146e9fd40a7feb10f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>聚合函数、 CALC 函数中和 NEW 关键字
数据成型支持以下功能。 分配给包含此列的章节来操作的名称是*章别名*。  
  
 章别名可以是完全限定，从而导致章包含每个章节列名称包含*列名，*各项之间由句点。 例如，如果父章，chap1，包含子章节，chap2，具有量列中，amt，则的限定的名称将为 chap1.chap2.amt。  
  
|聚合函数|Description|  
|-------------------------|-----------------|  
|SUM (*章别名*。*列名称*)|计算指定列中的所有值的总和。|  
|AVG (*章别名*。*列名称*)|计算指定列中的所有值的平均值。|  
|最大 (*章别名*。*列名称*)|计算指定的列中的最大值。|  
|最小值 (*章别名*。*列名称*)|计算指定列中的最小值。|  
|计数 (*章别名*[。*列名称*])|对指定的别名中的行数进行计数。 如果指定了某列，该列个为非 Null 的唯一行计数中包括。|  
|STDEV (*章别名*。*列名称*)|计算指定列中的标准偏差。|  
|任何 (*章别名*。*列名称*)|指定列的值。 仅当列的值是相同的章节中的所有行时，任何具有可预测的值。<br /><br /> **请注意**如果列不包含所有章节中的行的相同值，该形状命令任意返回的值进行任何函数的值之一。|  
  
|计算的表达式|Description|  
|---------------------------|-----------------|  
|CALC(*expression*)|计算的任意表达式，但只能在的行上**记录集**包含 CALC 函数。 使用这些任何表达式[Visual Basic for Applications (VBA) 函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)允许。|  
  
|NEW 关键字|Description|  
|-----------------|-----------------|  
|新*字段类型*[(*宽度* &#124; *缩放* &#124; *精度* &#124; *错误*[，*缩放* &#124; *错误*])]|将添加到指定的类型的空列**记录集**。|  
  
 *字段类型*传递与新的关键字可以是任何以下数据类型。  
  
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
|DBTYPE_BYTES|adBinary，感，adLongVarBinary|  
|DBTYPE_STR|每，以便您可以排除 adLongVarChar|  
|DBTYPE_WSTR|adWChar，adVarWChar adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 （OLE DB 中，DBTYPE_DECIMAL，或在 ADO，adDecimal） 十进制类型的新字段时，你必须指定的精度和小数位数的值。  
  
## <a name="see-also"></a>另请参阅  
 [调整示例数据](../../../ado/guide/data/data-shaping-example.md)   
 [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
