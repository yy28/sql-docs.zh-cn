---
title: CopyRecord 方法 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1d70dcba3d373b195950f90b6ef82c3d670844bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309205"
---
# <a name="copyrecord-method-ado"></a>CopyRecord 方法 (ADO)
将复制所表示的实体[记录](../../../ado/reference/ado-api/record-object-ado.md)到另一个位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 可选。 一个**字符串**值，该值包含指定实体的 URL 复制 （例如，文件或目录）。 如果*源*省略或指定一个空字符串、 文件或目录由当前[记录](../../../ado/reference/ado-api/record-object-ado.md)将被复制。  
  
 *目标*  
 可选。 一个**字符串**值，该值包含指定的位置的 URL 位置*源*将被复制。  
  
 *UserName*  
 可选。 一个**字符串**值，该值包含必要时，授予的访问权限的用户 ID*目标*。  
  
 *密码*  
 可选。 一个**字符串**值，该值包含密码，如果需要请验证是否*用户名*。  
  
 *选项*  
 可选。 一个[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)值，该值具有默认值为**adCopyUnspecified**。 指定此方法的行为。  
  
 *Async*  
 可选。 一个**布尔**值，当**True**，指定此操作应为异步。  
  
## <a name="return-value"></a>返回值  
 一个**字符串**通常返回的值的值*目标*。 但是，返回的确切值与提供程序相关。  
  
## <a name="remarks"></a>备注  
 值*源*并*目标*不能完全相同; 否则为将发生运行时错误。 在至少一个服务器、 路径或资源名称必须不同。  
  
 所有子项 （例如，子目录） 的*源*是复制以递归方式，除非**adCopyNonRecursive**指定。 在递归操作中，*目标*不能的子目录*源*; 否则为将无法完成该操作。  
  
 如果此方法将失败*目标*标识现有实体 （例如，文件或目录），除非**adCopyOverWrite**指定。  
  
> [!IMPORTANT]
>  使用**adCopyOverWrite**明智地选项。 例如，将文件复制到一个目录时指定此选项将*删除*目录，并替换该文件。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
