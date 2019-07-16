---
title: MoveRecord 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 157e38c2c9c23ff8f7e92af40385b0962c6dcb70
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918077"
---
# <a name="moverecord-method-ado"></a>MoveRecord 方法 (ADO)
将表示的实体[记录](../../../ado/reference/ado-api/record-object-ado.md)到另一个位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 可选。 一个**字符串**值，该值包含 URL 标识**记录**要移动。 如果*源*省略或指定了空字符串，表示此对象**记录**移动。 例如，如果**记录**表示一个文件，该文件的内容移动到指定的位置*目标*。  
  
 *目标*  
 可选。 一个**字符串**值，该值包含指定的位置的 URL 位置*源*将移动。  
  
 *UserName*  
 可选。 一个**字符串**值，该值包含必要时，授予的访问权限的用户 ID*目标*。  
  
 *密码*  
 可选。 一个**字符串**，其中包含的密码，如果需要请验证是否*用户名*。  
  
 *选项*  
 可选。 一个[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)值，其默认值为**adMoveUnspecified**。 指定此方法的行为。  
  
 *Async*  
 可选。 一个**布尔**值，当**True**，指定此操作应为异步。  
  
## <a name="return-value"></a>返回值  
 一个字符串值  。 通常情况下，值*目标*返回。 但是，返回的确切值与提供程序相关。  
  
## <a name="remarks"></a>备注  
 值*源*并*目标*不能完全相同; 否则为将发生运行时错误。 至少必须在不同的服务器、 路径和资源的名称。  
  
 对于使用 Internet 发布提供程序移动文件，此方法会更新正在移动，除非另有指定的文件中的所有超文本链接*选项*。 如果此方法将失败*目标*标识现有对象 （例如，文件或目录），除非**adMoveOverWrite**指定。  
  
> [!NOTE]
>  使用**adMoveOverWrite**明智地选项。 例如，将文件移到一个目录时指定此选项将删除该目录并替换的文件。  
  
 某些属性**记录**对象，例如[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)属性，此操作完成后将不会更新。 刷新**记录**对象的属性通过关闭**记录**，然后重新打开它使用已移动的文件或目录的位置的 URL。  
  
 如果此**记录**来自[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)，将不会立即在反映移动的文件或目录的新位置**记录集**。 刷新**记录集**通过关闭并重新打开它。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)
