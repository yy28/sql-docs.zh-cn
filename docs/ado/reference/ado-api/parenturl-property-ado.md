---
title: ParentURL 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 65704cea2a396e0f03de4bbcdc9f031f4c9af583
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703465"
---
# <a name="parenturl-property-ado"></a>ParentURL 属性 (ADO)
指示指向父级的绝对 URL 字符串[记录](../../../ado/reference/ado-api/record-object-ado.md)的当前**记录**对象。  
  
## <a name="return-value"></a>返回值  
 返回**字符串**值，该值指示父 URL**记录**。  
  
## <a name="remarks"></a>备注  
 **ParentURL**属性取决于用来打开源**记录**对象。 例如，**记录**可以使用包含引用的目录的相对路径名称的源打开[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性。  
  
 假定一个文件夹包含"first"下的"第二个"。 打开**记录**对象通过使用以下语法：  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 现在的值`the` **ParentURL**属性是`"https://first"`，则与相同**ActiveConnection**。  
  
 源也可以是绝对 URL 如， `"https://first/second"`。 **ParentURL**属性，即`"https://first"`，上面的层`"second"`。  
  
 如果此属性可能为 null 值：  
  
-   当前对象; 没有父级例如，如果**记录**对象表示目录的根目录。  
  
-   **记录**对象都表示不能使用 URL 指定的实体。  
  
 该属性为只读。  
  
> [!NOTE]
>  此属性仅支持由文档源提供程序，如[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[记录和提供程序提供字段](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
> [!NOTE]
>  如果当前记录中包含的数据记录从 ADO**记录集**，则访问**ParentURL**属性会导致运行时错误，指示，可能会没有 URL。  
  
## <a name="applies-to"></a>适用范围  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
