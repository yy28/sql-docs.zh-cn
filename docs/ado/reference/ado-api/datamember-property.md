---
title: "DataMember 属性 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset20::DataMember
helpviewer_keywords: DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e16e816b85cb6ccd35c40a15822f714f41215323
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="datamember-property"></a>DataMember 属性
指示将从检索的数据成员的名称[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)所引用的[数据源](../../../ado/reference/ado-api/datasource-property-ado.md)属性。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**值。 名称不区分大小写。  
  
## <a name="remarks"></a>注释  
 此属性用于与数据环境中创建数据绑定控件。 数据环境负责维护的包含的数据 （数据源） 的集合命名对象 （数据成员） 将表示为[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
 **DataMember**和**数据源**属性必须一起使用。  
  
 **DataMember**属性确定指定的对象**数据源**属性将表示为**记录集**对象。 **记录集**对象必须先关闭，然后设置此属性。 如果生成错误**DataMember**之前未设置属性**数据源**属性，或者如果**DataMember**中指定的对象无法识别名**数据源**属性。  
  
## <a name="usage"></a>用法  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [DataSource 属性 (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
