---
description: Source 属性（ADO 记录集）
title: ADO 记录集)  (源属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 3a71efe111a58ab8f799db512e77da4365ba5f48
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988898"
---
# <a name="source-property-ado-recordset"></a>Source 属性（ADO 记录集）
指示 [记录集](./recordset-object-ado.md) 对象的数据源。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置**字符串**值或[命令](./command-object-ado.md)对象引用;仅返回一个指示**记录集**的源的**字符串**值。  
  
## <a name="remarks"></a>注解  
 使用 **Source** 属性可以通过以下方法之一指定 **记录集** 对象的数据源： **命令** 对象变量、SQL 语句、存储过程或表名。  
  
 如果将**Source**属性设置为**Command**对象，则**Recordset**对象的[ActiveConnection](./activeconnection-property-ado.md)属性将继承指定**命令**对象的**ActiveConnection**属性的值。 但是，读取**源**属性不会返回**命令**对象;相反，它将返回您为其设置**源**属性的**命令**对象的[CommandText](./commandtext-property-ado.md)属性。  
  
 如果 **Source** 属性是 SQL 语句、存储过程或表名，则可以通过将相应的 *Options* 参数传递给 [Open](./open-method-ado-recordset.md) 方法调用来优化性能。  
  
 对于已关闭的**记录集**对象，**源**属性是可读/写的，对于打开的**记录集**对象是只读的。  
  
## <a name="applies-to"></a>适用于  
 [记录集对象 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Source 属性示例 (VB) ](./source-property-example-vb.md)   
 [ (ADO 错误的源属性) ](./source-property-ado-error.md)   
 [Source 属性（ADO 记录）](./source-property-ado-record.md)