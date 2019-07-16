---
title: 用于 Oracle 的 Microsoft OLE DB 提供程序 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926621"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle 概述
> [!IMPORTANT]
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用 Oracle 的 OLE DB 访问接口。

 Microsoft OLE DB Provider for Oracle 允许 ADO 来访问 Oracle 数据库。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到此提供程序，请设置*提供程序*的参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性设置为：

```vb
MSDAORA
```

 读取[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性将返回此字符串的形式。

 如果 Oracle 数据库中执行联接查询与 keyset 或 dynamic 游标，则将会出错。 Oracle 仅支持静态只读游标。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型的连接字符串是：

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 该字符串包含这些关键字：

|关键字|描述|
|-------------|-----------------|
|**提供程序**|指定适用于 Oracle 的 OLE DB 访问接口。|
|**数据源**|指定的服务器的名称。|
|**用户 ID**|指定用户名称。|
|**密码**|指定用户密码。|

> [!NOTE]
>  如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码在连接字符串中的信息。

## <a name="provider-specific-connection-parameters"></a>提供程序特定的连接参数
 此提供程序支持除 ADO 定义的多个提供程序特定的连接参数。 如使用 ADO 连接属性，可以通过设置这些特定于提供程序的属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)系列[连接](../../../ado/reference/ado-api/connection-object-ado.md)或作为的一部分**ConnectionString**.

 这些参数是完全中所述[OLE DB 程序员参考](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)。 [ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)提供这些参数名称和相应的 OLE DB 属性之间的交叉引用。

|参数|描述|
|---------------|-----------------|
|**窗口句柄**|指示要用于提示输入其他信息的窗口句柄。|
|**区域设置标识符**|指示唯一的 32 位数字 （例如 1033年），指定与用户的语言首选项。 这些首选项指示如何格式化日期和时间，项的按字母顺序排序，字符串进行了比较，依此类推。|
|**OLE DB 服务**|指示指定 OLE DB 服务启用或禁用的位掩码。|
|**提示**|指示是否提示用户，而所建立的连接。|
|**扩展的属性**|一个包含特定于访问接口字符串扩展的连接信息。 此属性仅用于不能通过属性机制所述的特定于提供程序的连接信息。|

## <a name="see-also"></a>请参阅
 [ConnectionString 属性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [提供程序属性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
