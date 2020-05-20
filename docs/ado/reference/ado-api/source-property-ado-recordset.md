---
title: Source 属性（ADO 记录集） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::putref_Source
- Recordset15::Source
- Recordset15::PutSource
- Recordset15::get_Source
- Recordset15::GetSource
- Recordset15::PutRefSource
- Recordset15::put_Source
helpviewer_keywords:
- Source property [ADO Recordset]
ms.assetid: a05ba2c9-2821-4343-8607-4de9b764ec91
author: rothja
ms.author: jroth
ms.openlocfilehash: fc7d3336b9c346a070266b4ef1d104d0e32eb042
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759803"
---
# <a name="source-property-ado-recordset"></a>Source 属性（ADO 记录集）
指示[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象的数据源。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置**字符串**值或[命令](../../../ado/reference/ado-api/command-object-ado.md)对象引用;仅返回一个指示**记录集**的源的**字符串**值。  
  
## <a name="remarks"></a>备注  
 使用**Source**属性可以通过以下方法之一指定**记录集**对象的数据源：**命令**对象变量、SQL 语句、存储过程或表名。  
  
 如果将**Source**属性设置为**Command**对象，则**Recordset**对象的[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性将继承指定**命令**对象的**ActiveConnection**属性的值。 但是，读取**源**属性不会返回**命令**对象;相反，它将返回您为其设置**源**属性的**命令**对象的[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性。  
  
 如果**Source**属性是 SQL 语句、存储过程或表名，则可以通过将相应的*Options*参数传递给[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法调用来优化性能。  
  
 对于已关闭的**记录集**对象，**源**属性是可读/写的，对于打开的**记录集**对象是只读的。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Source 属性示例（VB）](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Source 属性（ADO 错误）](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 属性（ADO 记录）](../../../ado/reference/ado-api/source-property-ado-record.md)
