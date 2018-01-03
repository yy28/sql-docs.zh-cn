---
title: "CopyRecord 方法 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords: CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 50749d088c57754ef9b667b114da8fb4f475ad19
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="copyrecord-method-ado"></a>CopyRecord 方法 (ADO)
将复制所表示的实体[记录](../../../ado/reference/ado-api/record-object-ado.md)到另一个位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 可选。 A**字符串**值，该值包含指定实体的 URL 要复制 （例如，文件或目录）。 如果*源*省略或指定一个空字符串、 文件或目录表示由当前[记录](../../../ado/reference/ado-api/record-object-ado.md)将被复制。  
  
 *目标*  
 可选。 A**字符串**值，该值包含指定的位置的 URL 其中*源*将被复制。  
  
 *UserName*  
 可选。 A**字符串**包含如果需要授予访问权限的用户 ID 值*目标*。  
  
 *密码*  
 可选。 A**字符串**值，该值包含的密码，如果需要请验证*用户名*。  
  
 *选项*  
 可选。 A [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)值，默认值为**adCopyUnspecified**。 指定此方法的行为。  
  
 *异步*  
 可选。 A**布尔**值，当**True**，指定应异步此操作。  
  
## <a name="return-value"></a>返回值  
 A**字符串**通常返回的值的值*目标*。 但是，返回的确切值与提供程序相关。  
  
## <a name="remarks"></a>Remarks  
 值*源*和*目标*不能完全相同; 否则为将发生运行时错误。 至少一个服务器、 路径或资源名称必须不同。  
  
 所有子级 （例如，子目录）*源*是复制以递归方式，除非**adCopyNonRecursive**指定。 在递归操作中，*目标*不得的子目录*源*; 否则为将无法完成该操作。  
  
 如果此方法将失败*目标*标识现有实体 （例如，文件或目录），除非**adCopyOverWrite**指定。  
  
> [!IMPORTANT]
>  使用**adCopyOverWrite**谨慎地选项。 例如，在将文件复制到目录时指定此选项将*删除*目录并将其替换该文件。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
