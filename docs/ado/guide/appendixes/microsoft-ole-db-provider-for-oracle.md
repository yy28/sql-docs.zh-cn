---
title: Oracle 的 Microsoft OLE DB 提供程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60510302525562d9c3007a6ef57213fc261b4c60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926621"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Oracle 的 Microsoft OLE DB 提供程序概述
> [!IMPORTANT]
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 的 OLE DB 提供程序。

 Oracle 的 Microsoft OLE DB 提供程序允许 ADO 访问 Oracle 数据库。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到该提供程序，请将[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性的*provider*参数设置为：

```vb
MSDAORA
```

 读取[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性也会返回此字符串。

 如果在 Oracle 数据库中执行具有键集或动态游标的联接查询，则会发生错误。 Oracle 仅支持静态的只读游标。

## <a name="typical-connection-string"></a>典型连接字符串
 此提供程序的典型连接字符串是：

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 字符串包含以下关键字：

|关键字|说明|
|-------------|-----------------|
|**提供程序**|指定 Oracle 的 OLE DB 提供程序。|
|**数据源**|指定服务器的名称。|
|**用户 ID**|指定用户名。|
|**权限**|指定用户密码。|

> [!NOTE]
>  如果要连接到支持 Windows 身份验证的数据源提供程序，应在连接字符串中指定**Trusted_Connection = yes**或**集成安全性 = SSPI**而不是用户 ID 和密码信息。

## <a name="provider-specific-connection-parameters"></a>特定于提供程序的连接参数
 提供程序除 ADO 定义的连接参数外，还支持多个特定于提供程序的连接参数。 与 ADO 连接属性一样，这些特定于提供程序的属性可通过[连接](../../../ado/reference/ado-api/connection-object-ado.md)的[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合或**ConnectionString**的一部分进行设置。

 这些参数在[OLE DB 程序员参考](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)中进行了充分介绍。 [ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)在这些参数名称和相应的 OLE DB 属性之间提供交叉引用。

|参数|说明|
|---------------|-----------------|
|**窗口句柄**|指示用于提示输入其他信息的窗口句柄。|
|**区域设置标识符**|指示一个唯一的32位数字（例如，1033），指定与用户语言相关的首选项。 这些首选项指示如何设置日期和时间的格式、按字母顺序对项进行排序、比较字符串，等等。|
|**OLE DB 服务**|指示一个位掩码，该位掩码指定要启用或禁用 OLE DB 服务。|
|**处**|指示在建立连接时是否提示用户。|
|**扩展属性**|包含特定于提供程序的扩展连接信息的字符串。 此属性仅用于特定于提供程序的连接信息，不能通过属性机制进行描述。|

## <a name="see-also"></a>另请参阅
 [ConnectionString 属性（ado）](../../../ado/reference/ado-api/connectionstring-property-ado.md) [提供程序属性（ado）](../../../ado/reference/ado-api/provider-property-ado.md) [记录集对象（ado）](../../../ado/reference/ado-api/recordset-object-ado.md)
