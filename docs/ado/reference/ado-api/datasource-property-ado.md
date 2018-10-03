---
title: 数据源属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataSource
helpviewer_keywords:
- DataSource property [ADO]
ms.assetid: 300a702a-3544-48c5-b759-83b511fe97e0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad42ea14e58e28bf5eee0e5aac66c5a8fc309f2f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801271"
---
# <a name="datasource-property-ado"></a>DataSource 属性 (ADO)
指示一个对象，包含数据而无法表示为[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="remarks"></a>备注  
 此属性用于数据环境下创建数据绑定控件。 数据环境负责维护数据 （数据源） 包含集合的命名对象 （数据成员） 将表示为**记录集**对象 *。*  
  
 [DataMember](../../../ado/reference/ado-api/datamember-property.md)并**数据源**属性必须结合使用。  
  
 所引用的对象必须实现**IDataSource**接口，并必须包含**IRowset**接口。  
  
## <a name="usage"></a>用法  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [DataMember 属性](../../../ado/reference/ado-api/datamember-property.md)
