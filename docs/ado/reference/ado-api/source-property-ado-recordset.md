---
title: "Source 属性 （ADO 记录集） |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ea45eae107fa55355adeb195e7e4fc5cf0a3c762
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="source-property-ado-recordset"></a>源属性 （ADO 记录集）
指示的数据源[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 集**字符串**值或[命令](../../../ado/reference/ado-api/command-object-ado.md)对象引用; 仅返回**字符串**值，该值指示的源**记录集**。  
  
## <a name="remarks"></a>注释  
 使用**源**属性指定的数据源**记录集**对象使用以下项之一：**命令**对象变量、 一个 SQL 语句、 存储的过程，或表名称。  
  
 如果你设置**源**属性**命令**对象， [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性**记录集**对象将继承值**ActiveConnection**属性指定**命令**对象。 但是，读取**源**属性不返回**命令**对象; 相反，它将返回[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性**命令**对象转换为其设置**源**属性。  
  
 如果**源**属性为 SQL 语句、 存储的过程或表名称，你可以通过传递相应优化性能*选项*参数与[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法调用。  
  
 **源**属性是读/写关闭**记录集**对象和只读打开**记录集**对象。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [源属性示例 (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [源属性 （ADO 错误）](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [源属性 （ADO 记录）](../../../ado/reference/ado-api/source-property-ado-record.md)
