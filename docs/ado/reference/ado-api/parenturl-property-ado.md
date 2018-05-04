---
title: ParentURL 属性 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51a7a476352519f4756e4e8f19166aac3c84d7da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="parenturl-property-ado"></a>ParentURL 属性 (ADO)
指示指向父级的绝对 URL 字符串[记录](../../../ado/reference/ado-api/record-object-ado.md)的当前**记录**对象。  
  
## <a name="return-value"></a>返回值  
 返回**字符串**值，该值指示的父 URL**记录**。  
  
## <a name="remarks"></a>注释  
 **ParentURL**属性取决于用来打开源**记录**对象。 例如，**记录**可以与源包含引用的目录的相对路径名打开[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性。  
  
 假设一个文件夹包含在"first"之下的"第二个"。 打开**记录**对象通过使用以下语法：  
  
```  
record.ActiveConnection = "http://first"  
record.Open "second"  
```  
  
 现在，值`the` **ParentURL**属性是`"http://first"`，与相同**ActiveConnection**。  
  
 源还可以是绝对 URL 如`"http://first/second"`。 **ParentURL**属性是然后`"http://first"`，上面的层`"second"`。  
  
 如果此属性可能为 null 的值：  
  
-   没有为当前的对象; 父级例如，如果**记录**对象表示目录的根目录。  
  
-   **记录**对象表示不能使用 URL 指定的实体。  
  
 该属性为只读。  
  
> [!NOTE]
>  此属性仅受文档源提供程序，如[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[记录和提供程序提供字段](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
> [!NOTE]
>  如果当前记录包含来自 ADO 的数据记录**记录集**，则访问**ParentURL**属性会导致运行时错误，指示可能会没有 URL。  
  
## <a name="applies-to"></a>适用范围  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
