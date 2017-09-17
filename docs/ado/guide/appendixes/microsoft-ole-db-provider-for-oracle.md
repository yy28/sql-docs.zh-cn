---
title: "Microsoft OLE DB Provider for Oracle |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d92236375a3ac152dbe7f5a2f259ce2a5f2edb79
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle 概述
> [!IMPORTANT]
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 的 OLE DB 访问接口。

 Microsoft OLE DB Provider for Oracle 允许 ADO 来访问 Oracle 数据库。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到此提供程序，设置*提供程序*参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性：

```
MSDAORA
```

 读取[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性将返回此字符串以及。

 如果 Oracle 数据库中执行联接查询包含由键集或动态游标，则将发生错误。 Oracle 仅支持静态只读游标。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型连接字符串是：

```
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 该字符串包含这些关键字：

|关键字|Description|
|-------------|-----------------|
|**提供程序**|指定适用于 Oracle 的 OLE DB 访问接口。|
|**数据源**|指定服务器的名称。|
|**用户 ID**|指定的用户名。|
|**密码**|指定的用户密码。|

> [!NOTE]
>  如果你要连接到的数据源提供程序支持 Windows 身份验证，你应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码连接字符串中的信息。

## <a name="provider-specific-connection-parameters"></a>提供程序特定的连接参数
 提供程序支持除 ADO 所定义的多个提供程序特定的连接参数。 如使用 ADO 连接属性，可以通过设置这些提供程序特定属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合[连接](../../../ado/reference/ado-api/connection-object-ado.md)或作为的一部分**ConnectionString**.

 这些参数可全面地描述了在[OLE DB 程序员参考](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)。 [ADO 动态属性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)提供这些参数名称和相应的 OLE DB 属性之间的交叉引用。

|参数|Description|
|---------------|-----------------|
|**窗口句柄**|指示要用于提示输入其他信息的窗口句柄。|
|**区域设置标识符**|指示唯一的 32 位数字 （例如 1033年），指定与用户的语言首选项。 这些首选项指示如何格式化日期和时间，项按字母顺序排列，字符串进行比较，依次类推。|
|**OLE DB 服务**|指示指定 OLE DB 服务启用或禁用的位掩码。|
|**提示**|指示是否正在建立连接时提示用户。|
|**扩展的属性**|包含提供程序特定的扩展的连接信息的字符串。 此属性仅用于不能通过属性机制所述的提供程序特定的连接信息。|

## <a name="see-also"></a>另请参阅
 [ConnectionString 属性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [提供程序属性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

