---
title: DeleteRecord 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 409c4e21395b7b903cf4ff03726fbd37a2a218d1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67919085"
---
# <a name="deleterecord-method-ado"></a>DeleteRecord 方法 (ADO)
删除[记录](../../../ado/reference/ado-api/record-object-ado.md)表示的实体。  
  
## <a name="syntax"></a>语法  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>参数  
 *源*  
 可选。 一个**字符串**值，该值包含用于标识要删除的实体（例如，文件或目录）的 URL。 如果省略了*Source*或指定了空字符串，则将删除当前[记录](../../../ado/reference/ado-api/record-object-ado.md)表示的实体。 如果记录是集合记录（[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) of **adCollectionRecord**，例如目录），则所有子项（例如，子目录）也将被删除。  
  
 *异步*  
 可选。 一个**布尔**值，如果**为 True**，则指定删除操作为异步。  
  
## <a name="remarks"></a>备注  
 此方法完成后，对此**记录**所表示的对象执行的操作可能会失败。 在调用**DeleteRecord**之后，应关闭**记录**，因为**记录**的行为可能会因提供程序用数据源更新**记录**的时间而变得不可预知。  
  
 如果此**记录**是从[记录集中](../../../ado/reference/ado-api/recordset-object-ado.md)获取的，则此操作的结果不会立即反映在**记录集中**。 刷新记录集，方法是关闭然后重新打开该**记录集**，或者**执行 recordset** [Requery](../../../ado/reference/ado-api/requery-method.md)方法、 [Update](../../../ado/reference/ado-api/update-method.md)方法或重新[同步](../../../ado/reference/ado-api/resync-method.md)方法。  
  
> [!NOTE]
>  使用 http 方案的 Url 将自动调用[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>应用于  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Delete 方法（ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法（ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法（ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
