---
title: 源属性 （ADO 记录集） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 59a043b6258de83986e447c87209fa781a1ae352
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711115"
---
# <a name="source-property-ado-recordset"></a>Source 属性（ADO 记录集）
指示的数据源[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 集**字符串**值或[命令](../../../ado/reference/ado-api/command-object-ado.md)对象引用; 只返回**字符串**值，该值指示的源**记录集**。  
  
## <a name="remarks"></a>备注  
 使用**源**属性指定的数据源**记录集**对象使用以下值之一：**命令**对象变量、 SQL 语句、 存储的过程或表名称。  
  
 如果您设置**源**属性设置为**命令**对象， [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性的**记录集**对象将继承值**ActiveConnection**为指定的属性**命令**对象。 但是，读取**源**属性不会返回**命令**对象; 相反，它会返回[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性**命令**对象复制到其中设置**源**属性。  
  
 如果**源**属性为 SQL 语句、 存储的过程或表名，可以通过传递相应优化性能*选项*自变量与[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法调用。  
  
 **源**属性是读/写的关闭**记录集**对象和只读方式打开**记录集**对象。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Source 属性示例 (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [源属性 （ADO 错误）](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 属性（ADO 记录）](../../../ado/reference/ado-api/source-property-ado-record.md)
