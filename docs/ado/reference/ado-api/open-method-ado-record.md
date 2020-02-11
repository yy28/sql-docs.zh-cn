---
title: Open 方法（ADO 记录） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97c7f1c143c83dd35ca5ff17e9776d79fb734ff9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917925"
---
# <a name="open-method-ado-record"></a>Open 方法（ADO 记录）
打开现有[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，或创建由**记录**表示的新项，如文件或目录。  
  
## <a name="syntax"></a>语法  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>parameters  
 *数据源*  
 可选。 一种**变量**，该变量可以表示此**记录**对象所表示的实体的 URL、**命令**、打开的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)或其他**记录**对象、包含 SQL SELECT 语句或表名称的字符串。  
  
 *ActiveConnection*  
 可选。 一个表示连接字符串或打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象的**变量**。  
  
 *模式*  
 可选。 一个[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值，该值指定结果**记录**对象的访问模式。 默认值为**adModeUnknown**。  
  
 *CreateOptions*  
 可选。 一个[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)值，该值指定是否应打开现有的文件或目录，或创建新的文件或目录。 默认值为**adFailIfNotExists**。 如果设置为默认值，则将从[mode](../../../ado/reference/ado-api/mode-property-ado.md)属性获取访问模式。 如果*源*参数不包含 URL，则会忽略此参数。  
  
 *选项*  
 可选。 一个[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)值，该值指定用于打开**记录**的选项。 默认值为**adOpenRecordUnspecified**。 这些值可以组合在一起。  
  
 *用户名*  
 可选。 一个**字符串**值，该值包含用户 ID，该 ID 在需要时授予对*源*的访问权限。  
  
 *权限*  
 可选。 一个包含密码的**字符串**值（如果需要）将验证*用户名*。  
  
## <a name="remarks"></a>备注  
 *源*可能是：  
  
-   一个 URL。 如果 URL 的协议是 http，则默认情况下将调用 Internet 访问接口。 如果 URL 指向包含可执行脚本的节点（如），则为。ASP 页），则默认情况下会打开包含源而不是执行的内容的**记录**。 使用*Options*参数来修改此行为。  
  
-   **记录**对象。 从另一个**记录**打开的**记录**对象将克隆原始**记录**对象。  
  
-   **命令**对象。 已打开的**记录**对象表示通过执行**命令**返回的单个行。 如果结果包含多行，则将第一行的内容放在记录中，并将错误添加到**错误**集合中。  
  
-   一个 SQL SELECT 语句。 打开的**记录**对象表示通过执行字符串的内容返回的单个行。 如果结果包含多行，则将第一行的内容放在记录中，并将错误添加到**错误**集合中。  
  
-   表名称。  
  
 如果**Record**对象表示无法使用 URL 访问的实体（例如，从数据库派生的**记录集**的行），则[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)属性和使用**adRecordURL**常量访问的字段的值均为 null。  
  
> [!NOTE]
>  使用 http 方案的 Url 将自动调用[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>应用于  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Open 方法（ADO 连接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法（ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
