---
title: "Source 属性 （ADO 记录） |Microsoft 文档"
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
- _Record::Source
- _Record::PutRefSource
- _Record::GetSource
- _Record::put_Source
- _Record::putref_Source
- _Record::get_Source
helpviewer_keywords:
- Source property [ADO Record]
ms.assetid: 2c18279e-6f35-4af0-b12e-8f1543d9ed20
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 524845f59338a483df89586847157e6d9eaa598c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="source-property-ado-record"></a>源属性 （ADO 记录）
指示数据源或由表示对象[记录](../../../ado/reference/ado-api/record-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**Variant**值，该值指示所表示的实体**记录**。  
  
## <a name="remarks"></a>注释  
 **源**属性返回*源*参数**记录**对象[打开](../../../ado/reference/ado-api/open-method-ado-record.md)方法。 它可以包含一个绝对或相对 URL 字符串。 绝对 URL 可用但不包括设置[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性以直接打开**记录**对象。 一种隐式**连接**在这种情况下创建对象。  
  
 **源**属性还可以包含对已打开的引用**记录集**，这将打开**记录**表示中的当前行对象**记录集**。  
  
 **源**属性还可能包含对引用[命令](../../../ado/reference/ado-api/command-object-ado.md)从提供程序返回数据的单个行的对象。  
  
 如果**ActiveConnection**还设置属性，则**源**属性必须指向某个存在该连接的作用域内的对象。 例如，在树状命名空间中，如果**源**属性包含一个绝对 URL，则必须指向在由连接字符串中的 URL 标识的节点范围内存在的节点。 如果**源**属性包含相对 URL，然后通过设置的上下文中验证**ActiveConnection**属性。  
  
 **源**属性为读/写时**记录**对象已关闭，并且为只读时**记录**对象处于打开状态。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [源属性 （ADO 错误）](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [源属性 （ADO 记录集）](../../../ado/reference/ado-api/source-property-ado-recordset.md)

