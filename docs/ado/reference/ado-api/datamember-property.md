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
ms.openlocfilehash: 623f9b1f1e8873ddc4819bb8500c11edf09f5f76
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67919223"
---
# <a name="datamember-property"></a>DataMember 属性
指示将从[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)属性所引用的[记录集中](../../../ado/reference/ado-api/recordset-object-ado.md)检索的数据成员的名称。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个**字符串**值。 该名称不区分大小写。  
  
## <a name="remarks"></a>备注  
 此属性用于通过数据环境创建数据绑定控件。 数据环境维护数据集合（数据源），其中包含将表示为[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象的命名对象（数据成员）。  
  
 **DataMember**和**DataSource**属性必须一起使用。  
  
 **DataMember**属性确定由**DataSource**属性指定的哪个对象将表示为**记录集**对象。 必须先关闭**Recordset**对象，然后才能设置此属性。 如果在**datasource**属性之前未设置**datamember**属性，或者**数据源**属性中指定的对象无法识别**datamember**名称，则会生成错误。  
  
## <a name="usage"></a>使用情况  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [DataSource 属性 (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
