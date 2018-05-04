---
title: 移动记录方法 (ADO) |Microsoft 文档
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
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 103206f4f4fe731da23a194cf89a54a404545f0d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="moverecord-method-ado"></a>移动记录方法 (ADO)
将移动所表示的实体[记录](../../../ado/reference/ado-api/record-object-ado.md)到另一个位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 選擇性。 A**字符串**值，该值包含 URL 标识**记录**要移动。 如果*源*省略或指定空字符串，表示此对象**记录**移动。 例如，如果**记录**表示一个文件，文件的内容移到指定的位置*目标*。  
  
 *目标*  
 選擇性。 A**字符串**值，该值包含指定的位置的 URL 其中*源*将移动。  
  
 *UserName*  
 選擇性。 A**字符串**包含如果需要授予访问权限的用户 ID 值*目标*。  
  
 *密码*  
 選擇性。 A**字符串**包含的密码，如果需要请验证*用户名*。  
  
 *Options*  
 選擇性。 A [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)值其默认值为**adMoveUnspecified**。 指定此方法的行为。  
  
 *异步*  
 選擇性。 A**布尔**值，当**True**，指定此操作应为异步。  
  
## <a name="return-value"></a>返回值  
 A**字符串**值。 通常情况下，值*目标*返回。 但是，返回的确切值与提供程序相关。  
  
## <a name="remarks"></a>注释  
 值*源*和*目标*不能完全相同; 否则为将发生运行时错误。 至少的服务器、 路径和资源的名称必须不同。  
  
 对于使用 Internet 发布提供程序移动的文件，此方法更新正在移，除非另有指定的文件中的所有超文本链接*选项*。 如果此方法将失败*目标*标识现有对象 （例如，文件或目录），除非**adMoveOverWrite**指定。  
  
> [!NOTE]
>  使用**adMoveOverWrite**谨慎地选项。 例如，在将文件移到目录时指定此选项将删除该目录并将其替换该文件。  
  
 某些属性**记录**对象，如[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)属性，此操作完成后将不会更新。 刷新**记录**对象的属性通过关闭**记录**，然后重新打开它使用的文件或目录已移到的位置的 URL。  
  
 如果此**记录**通过[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，移动的文件或目录的新位置将不会立即反映到**记录集**。 刷新**记录集**通过关闭并重新打开它。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)
