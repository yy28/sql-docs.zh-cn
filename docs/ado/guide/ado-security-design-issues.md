---
title: "ADO 安全设计问题 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: "“drivers”"
ms.topic: article
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 51c7e3cf9c99bdd76ce1b84a7c387b1e6e4d2f58
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="ado-security-design-features"></a>ADO 安全设计功能
下列各节描述安全设计功能在 ActiveX 数据对象 (ADO) 2.8 及更高版本。 ADO 2.8 中做了这些更改以提高安全性。 ADO 6.0 中，包括在 Windows Vista 中的 Windows DAC 6.0 中，在功能上等效于 ADO 2.8，它包括在 Windows XP 和 Windows Server 2003 中的 MDAC 2.8。 本主题提供有关如何最好地保护你的应用程序在 ADO 2.8 或更高版本中的信息。

> [!IMPORTANT]
>  如果你要更新你的应用程序从早期版本的 ADO，建议你测试更新的应用程序在非生产计算机上，然后将其部署到客户。 这样一来，你可以确保在部署更新的应用程序之前，你不了解的任何兼容性问题。

## <a name="internet-explorer-file-access-scenarios"></a>Internet 资源管理器文件访问方案
 当在中使用 ADO 2.8 及更高版本的工作原理的以下功能效果编写脚本在 Internet Explorer 中的网页。

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>修改后的、 经过改进的安全警告消息框现在用于警报的用户
 ADO 2.7 及更早版本中，对于以下警告消息将显示当已编写脚本的 Web 页上尝试运行中的不受信任的提供程序的 ADO 代码：

```
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 为 ADO 2.8 及更高版本中，前面的消息不会再出现。 相反，在此上下文中将显示以下消息：

```
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 前面的消息，用户可以做出明智的决策，同时了解这两个选项的后果：

-   如果用户信任该站点，单击确定将允许所有磁盘安全代码 （所有 ADO 方法和属性在本主题后面所述的磁盘访问 Api 的情况除外） 运行，并在浏览器窗口中执行。

-   如果用户不信任该站点，单击取消阻止来自运行，而且在整个中执行数据访问的 ADO 代码。

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>现在限定为受信任的站点的可访问磁盘的代码
 ADO 专门限制的一组有限的 Api，它可能会公开可能从读取或写入到本地计算机上的文件的能力的 2.8 中做了额外的设计更改。 此处列出的 API 方法已进一步限制为安全起见，在运行 Internet Explorer 时：

-   ADO 的**流**对象，如果[LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md)或[SaveToFile](../../ado/reference/ado-api/savetofile-method.md)方法使用。

-   ADO 的**记录集**对象，如果任一[保存](../../ado/reference/ado-api/save-method.md)方法或[打开](../../ado/reference/ado-api/open-method-ado-recordset.md)方法，例如，当任一**adCmdFile**选项设置或[Microsoft OLE DB 永久性提供程序 (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)使用。

 对于这些有限的可能磁盘可访问的函数集，以下行为进行 ADO 2.8 及更高版本，如果在 Internet Explorer 中运行使用这些方法的任何代码：

-   如果提供的代码的站点之前添加到受信任的站点区域列表，在浏览器中执行的代码并授予对本地文件的访问。

-   如果在受信任的站点区域列表中不出现站点，代码会阻止，并且对本地文件的访问被拒绝。

    > [!NOTE]
    >  在 ADO 2.8 及更高版本中，用户未发出警报或建议将站点添加到受信任的站点区域列表。 因此的受信任的站点列表管理是用户部署或支持基于网站的应用程序需要访问本地文件系统的用户的责任。

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>阻止到记录集对象上的 ActiveCommand 属性访问
 Internet Explorer 中运行时，ADO 2.8 现在阻止对访问权限[ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md)为活动的属性**记录集**对象并返回错误。 无论页是否来自受信任的站点列表中注册网站发生此错误。

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>有关 OLE DB 提供程序和集成的安全性的处理中的更改
 时查看 ADO 2.7 和潜在的安全问题和问题的更早版本，发现以下方案：

 在某些情况下，OLE DB 提供商支持集成安全性[DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx)属性可能会允许脚本化的 Web 页面，以重用无意中连接到其他服务器的 ADO 连接对象使用当前登录凭据的用户。 若要防止此情况，ADO 2.8 及更高版本，请处理 OLE DB 提供程序具体取决于如何选择它们，以提供，或未提供，集成安全性。

 对于从受信任的站点区域列表中列出的站点加载的网页下, 表提供 ADO 2.8 及更高版本如何管理每个用例中的 ADO 连接的细分。

|用户身份验证的 IE 设置登录|提供程序支持"集成安全性"和 UID 和 PWD 被指定 (SQLOLEDB)|提供程序不支持"Integrated Security"(震动，MSDASQL，MSPersist)|提供程序支持"Integrated Security"，它设置为 SSPI （指定没有 UID/PWD）|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|使用当前的用户名和密码自动登录|允许连接|允许连接|允许连接|
|提示输入用户名和密码|允许连接|失败连接|失败连接|
|只在 Intranet 区域自动登录|允许连接|提示用户与安全警告|提示用户与安全警告|
|匿名登录|允许连接|失败连接|失败连接|

 在安全警告现在出现的位置的情况下，消息框，通知用户：

```
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 前面的消息允许用户做出更明智的决策并进行相应处理。

> [!NOTE]
>  有关受信任的网站 （即，站点不受信任的站点区域列表中列出），如果提供程序也是不受信任 （如本节前面所述），用户可能会看到的行、 不安全的提供程序有关的警告和第二个警告中的两个安全警告尝试使用其标识。 如果用户单击确定，为第一个警告，Internet Explorer 设置和前面的表中所述的响应行为代码的执行。

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>控制是否在 ADO 连接字符串中返回密码文本
 当你尝试获取的值[ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md)属性 ADO**连接**对象时，会发生以下事件：

1.  如果连接为打开状态，初始化然后进行调用基础 OLE DB 访问接口来获取连接字符串。

2.  具体取决于的 OLE DB 提供程序中的设置[DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx)属性，密码是与返回其他连接字符串信息一起包括。

 例如，如果 ADO 连接动态属性**Persist Security Info**设置为**True**，返回的连接字符串中包含密码信息。 否则为如果基础提供程序已将属性设置为**False** （例如，使用 SQLOLEDB 访问接口），返回的连接字符串中省略密码信息。

 如果你使用第三方 (即，非 Microsoft) 通过 ADO 应用程序代码使用的 OLE DB 提供程序，您可以检查如何**DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO**实现属性来确定是否包含允许使用 ADO 连接字符串的密码信息。

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>在加载和保存记录集或流时的非文件设备检查
 ADO 2.7 及更早版本中，为文件输入/输出操作如[打开](../../ado/reference/ado-api/open-method-ado-recordset.md)和[保存](../../ado/reference/ado-api/save-method.md)用来读取和写入基于文件的数据可能在某些情况下允许的 URL 或文件名称用于指定非磁盘基于文件类型。 例如，LPT1，COM2，PRN。TXT、 AUX 可使用作为别名的打印机和辅助设备之间系统使用特定的输入/输出

 有关 ADO 2.8 及更高版本，此功能已进行更新。 用于打开和保存**记录集**和**流**对象，ADO 现在执行文件类型检查，以确保 URL 或文件名称中指定的输入或输出设备的实际文件。

> [!NOTE]
>  文件类型检查本部分中所述仅适用于 Windows 2000 和更高版本。 它不适用于 ADO 2.8 或更高版本在早期 Windows 版本中，如 Windows 98 正在其中运行的情况下。

