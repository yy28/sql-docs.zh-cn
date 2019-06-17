---
title: DataMember 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataMember
helpviewer_keywords:
- DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9de69478469a6bd177d12beab96e199b4720f3f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695483"
---
# <a name="datamember-property"></a>DataMember 属性
指示将从检索的数据成员的名称[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)所引用的[数据源](../../../ado/reference/ado-api/datasource-property-ado.md)属性。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**值。 名称不区分大小写。  
  
## <a name="remarks"></a>备注  
 此属性用于数据环境下创建数据绑定控件。 数据环境负责维护数据 （数据源） 包含集合的命名对象 （数据成员） 将表示为[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
 **DataMember**并**数据源**属性必须一起使用。  
  
 **DataMember**属性确定指定的对象**数据源**属性将表示为**记录集**对象。 **记录集**之前设置此属性，必须关闭对象。 如果生成错误**DataMember**属性未设置之前**数据源**属性，或者，如果**DataMember**中指定的对象无法识别名称**数据源**属性。  
  
## <a name="usage"></a>用法  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [DataSource 属性 (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
