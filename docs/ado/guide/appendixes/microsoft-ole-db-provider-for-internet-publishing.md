---
title: "用于 Internet 发布的 Microsoft OLE DB 提供程序 |Microsoft 文档"
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
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d466123e7330eb599847225d2b108ec7f80d9ea9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Microsoft OLE DB Provider for Internet 发布概述
Microsoft OLE DB 提供程序用于 Internet 发布允许 ADO 由 Microsoft FrontPage 或 Microsoft Internet 信息服务器提供服务的访问资源。 资源包括 web 源代码文件，例如 HTML 文件或 Windows 2000 web 文件夹。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到此提供程序，设置*提供程序*参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性：

```
MSDAIPP.DSO
```

 此值还可以设置或读取使用[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型连接字符串是：

```
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 - 或 -

```
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 该字符串包含这些关键字：

|关键字|Description|
|-------------|-----------------|
|**提供程序**|指定 Internet 发布的 OLE DB 访问接口。|
|**数据源**-或- **URL**|指定的文件或目录发布的 Web 文件夹中的 URL。|
|**用户 ID**|指定的用户名。|
|**密码**|指定的用户密码。|

> [!NOTE]
>  如果你要连接到的数据源提供程序支持 Windows 身份验证，你应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码连接字符串中的信息。

 如果你设置*ResourceURL*值从"URL ="值无效的连接字符串，在默认情况下 Internet 发布提供程序会引发一个对话框，提示输入有效的值。 这是中间层应用程序中的组件的意外行为，因为暂停程序执行，直到清除对话框中，客户端似乎会冻结因为它没有收到响应来自该组件。

> [!NOTE]
>  如果 MSDAIPP。DSO 显式指定的提供程序，使用值为*提供程序*连接字符串关键字或**提供程序**属性，不能使用"URL ="连接字符串中。 如果这样做，将会出错。 本主题中所示相反，只需指定 URL[与 OLE DB 提供程序用于 Internet 发布使用 ADO](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)。

## <a name="see-also"></a>另请参阅
 [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md) [Internet 发布的 OLE DB 访问接口](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)

