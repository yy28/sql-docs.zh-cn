---
title: ParentURL 属性（ADO） |Microsoft Docs
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
ms.openlocfilehash: 54b2db44fe2e1971356f96d33aa8de0b02781b1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931644"
---
# <a name="parenturl-property-ado"></a>ParentURL 属性 (ADO)
指示指向当前**记录**对象的父[记录](../../../ado/reference/ado-api/record-object-ado.md)的绝对 URL 字符串。  
  
## <a name="return-value"></a>返回值  
 返回一个**字符串**值，该值指示父**记录**的 URL。  
  
## <a name="remarks"></a>备注  
 **ParentURL**属性取决于用于打开**Record**对象的源。 例如，可以使用包含[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)属性引用的目录的相对路径名称的源打开**记录**。  
  
 假设 "second" 是包含在 "first" 下的文件夹。 使用以下语法打开**Record**对象：  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 现在， `the` **ParentURL**属性`"https://first"`的值与**ActiveConnection**相同。  
  
 源还可以是绝对 URL，如， `"https://first/second"`。 然后**** `"https://first"`，ParentURL 属性是上述`"second"`级别。  
  
 如果以下情况，此属性可能为 null 值：  
  
-   当前对象没有父对象;例如，如果**Record**对象表示目录的根。  
  
-   **Record**对象表示不能使用 URL 指定的实体。  
  
 此属性为只读。  
  
> [!NOTE]
>  此属性仅受文档源提供程序支持，例如[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[记录和提供程序提供的字段](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
> [!NOTE]
>  使用 http 方案的 Url 将自动调用[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
> [!NOTE]
>  如果当前记录包含 ADO**记录集**的数据记录，则访问**ParentURL**属性将导致运行时错误，指示不可能存在 URL。  
  
## <a name="applies-to"></a>应用于  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
