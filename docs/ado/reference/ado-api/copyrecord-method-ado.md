---
title: CopyRecord 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aaabb32234cefe2e3c3727ce5a18dd2d98549a77
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933419"
---
# <a name="copyrecord-method-ado"></a>CopyRecord 方法 (ADO)
将[记录](../../../ado/reference/ado-api/record-object-ado.md)表示的实体复制到其他位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>参数  
 *源*  
 可选。 一个**字符串**值，该值包含指定要复制的实体的 URL （例如，文件或目录）。 如果省略了*Source*或指定了空字符串，则将复制当前[记录](../../../ado/reference/ado-api/record-object-ado.md)所表示的文件或目录。  
  
 *目标*  
 可选。 一个**字符串**值，该值包含指定将复制*源*的位置的 URL。  
  
 *用户名*  
 可选。 一个**字符串**值，该值包含用户 ID，该 ID 在需要时授予访问*目标*的权限。  
  
 *密码*  
 可选。 一个包含密码的**字符串**值，如果需要，将验证*用户名*。  
  
 *选项*  
 可选。 默认值为**adCopyUnspecified**的[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)值。 指定此方法的行为。  
  
 *异步*  
 可选。 一个**布尔**值，如果**为 True，则**将此操作指定为异步。  
  
## <a name="return-value"></a>返回值  
 通常返回*Destination*值的**字符串**值。 但是，返回的确切值与提供程序相关。  
  
## <a name="remarks"></a>备注  
 *源*和*目标*的值不得完全相同;否则，会发生运行时错误。 至少一个服务器、路径或资源名称必须不同。  
  
 除非指定**adCopyNonRecursive** ，否则会以递归方式复制*源*的所有子元素（例如，子目录）。 在递归操作中，*目标*不能是*源*的子目录;否则，操作将不会完成。  
  
 如果*Destination*标识现有实体（例如文件或目录），则此方法将失败，除非指定了**adCopyOverWrite** 。  
  
> [!IMPORTANT]
>  谨慎使用**adCopyOverWrite**选项。 例如，如果在将文件复制到目录时指定此选项，则会*删除*该目录并将其替换为文件。  
  
> [!NOTE]
>  使用 http 方案的 Url 将自动调用[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>应用于  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
