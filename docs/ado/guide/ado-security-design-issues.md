---
title: ADO 安全设计问题 |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64f4a22d849572d6e32006dbe997dd134e5c2e0d
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "51293123"
---
# <a name="ado-security-design-features"></a>ADO 安全设计功能
以下各节介绍安全设计功能在 ActiveX 数据对象 (ADO) 2.8 和更高版本。 这些更改是在 ADO 中 2.8 为了提高安全性。 ADO 6.0 中，包含在 Windows Vista 中的 Windows DAC 6.0 中，是功能上等效于 ADO 2.8，它包括在 Windows XP 和 Windows Server 2003 中的 MDAC 2.8。 本主题提供有关如何最好地保护 ADO 2.8 或更高版本中的应用程序的信息。

> [!IMPORTANT]
>  如果要更新从早期版本的 ADO 应用程序，建议将其部署到客户之前测试更新的应用程序的非生产计算机上。 这样一来，可以确保在部署更新的应用程序之前已经知道的任何兼容性问题。

## <a name="internet-explorer-file-access-scenarios"></a>Internet Explorer 文件访问控制方案
 以下功能效果中使用时，ADO 2.8 和更高版本的工作方式编写的脚本在 Internet Explorer 中的网页。

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>现在，以提醒用户使用修改后的和改进的安全警告消息框
 ADO 2.7 和更早版本中，对于以下警告消息显示已编写脚本的 Web 页上尝试运行不受信任的提供程序中的 ADO 代码时：

```console
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 针对 ADO 2.8 和更高版本中，前面的消息不会再出现。 相反，在此上下文中将显示以下消息：

```console
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 前面的消息允许用户做出明智的决策，同时知道这两个选项的结果：

-   如果用户信任该站点，单击确定将允许所有磁盘安全代码 （所有 ADO 方法和属性在本主题后面所述的磁盘访问 Api 除外） 运行，并在浏览器窗口中执行。

-   如果用户不信任该站点，单击取消阻止从运行并完全执行的数据访问的 ADO 代码。

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>磁盘可访问的代码现在限定为受信任的站点
 在 ADO 中 2.8 专门限制的一组有限的 Api，这可能会读取或写入到本地计算机上的文件，可能会使功能进行了额外的设计更改。 以下是已被进一步的 API 方法限制为安全起见，运行 Internet Explorer 时：

-   有关 ADO **Stream**对象，如果[LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md)或[SaveToFile](../../ado/reference/ado-api/savetofile-method.md)使用方法。

-   ADO**记录集**对象，如果任一[保存](../../ado/reference/ado-api/save-method.md)方法或[打开](../../ado/reference/ado-api/open-method-ado-recordset.md)方法，例如何时任一**adCmdFile**选项设置或[Microsoft OLE DB 永久性提供程序 (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)使用。

 有关这些有限的磁盘可能会访问函数集，ADO 2.8 和更高版本，如果在 Internet Explorer 中运行使用这些方法的任何代码的出现以下行为：

-   如果提供的代码的站点之前添加到受信任的站点区域列表，在浏览器中执行的代码以及对本地文件授予访问权限。

-   如果站点不会出现在受信任的站点区域列表中，代码会阻止，并且对本地文件访问被拒绝。

    > [!NOTE]
    >  在 ADO 2.8 和更高版本中，用户不是向你发出警报或建议将站点添加到受信任的站点区域列表。 因此的受信任的站点列表管理是那些要部署或支持基于网站的应用程序需要访问本地文件系统的责任。

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>阻止到记录集对象上的 ActiveCommand 属性访问
 Internet Explorer 中运行时，ADO 2.8 现在阻止访问[ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md)活动的属性**记录集**对象并返回错误。 无论页面是否来自受信任的站点列表中注册网站发生此错误。

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>在处理中的 OLE DB 访问接口和集成的安全性的更改
 在查看 ADO 2.7 和更早版本的潜在安全问题和问题，发现以下方案：

 在某些情况下，OLE DB 访问接口支持集成安全性[DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx)属性可能有可能使已编写脚本的 Web 页以重复使用 ADO 连接对象无意中连接到其他服务器使用用户的当前登录凭据。 若要防止此情况，ADO 2.8 和更高版本，请处理 OLE DB 访问接口具体取决于如何选择它们，以提供，也不提供为使用集成安全性。

 从受信任的站点区域列表中列出的站点加载的网页下, 表提供了 ADO 2.8 和更高版本中每个用例的 ADO 连接的管理方式的明细。

|IE 设置进行用户身份验证登录|提供程序支持"集成安全性"和 UID 和 PWD 被指定 (SQLOLEDB)|提供程序不支持"Integrated Security"(JOLT，MSDASQL，MSPersist)|提供程序支持"集成安全性"，并且设置为 SSPI （指定没有 UID/PWD）|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|自动使用当前用户名和密码登录|允许连接|允许连接|允许连接|
|提示输入用户名和密码|允许连接|失败连接|失败连接|
|只在 Intranet 区域自动登录|允许连接|提示用户与安全警告|提示用户与安全警告|
|匿名登录|允许连接|失败连接|失败连接|

 安全警告现在的显示位置的情况下，在消息框，通知用户：

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 前面的消息允许用户做出更明智的决策并进行相应处理。

> [!NOTE]
>  不受信任网站 （即，网站不受信任的站点区域列表中列出），如果提供程序也不受信任 （如前面在本部分中所述），用户可能会看到的行、 不安全提供程序有关的警告和第二个警告中的两个安全警告尝试使用其标识。 如果用户单击确定进行的第一个警告，Internet Explorer 设置和前面的表中所述的响应行为代码的执行。

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>控制是否在 ADO 连接字符串中返回密码文本
 当你尝试获取的值[ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md)属性上 ADO**连接**对象时，会发生以下事件：

1.  如果连接处于打开状态，初始化然后调用基础 OLE DB 访问接口来获取连接字符串。

2.  具体取决于中的 OLE DB 访问接口设置[DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx)属性，密码是包含与返回的其他连接字符串信息。

 例如，如果 ADO 连接动态属性**Persist Security Info**设置为**True**，密码信息包括在返回的连接字符串。 否则为如果基础提供程序已将属性设置为**False** （例如使用 SQLOLEDB 访问接口），返回的连接字符串中省略密码信息。

 如果您使用的第三方 (即，非 Microsoft) OLE DB 访问接口使用 ADO 应用程序代码中，你可能会检查如何**DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO**实现属性以确定是否包含允许使用 ADO 连接字符串的密码信息。

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>适用于非文件设备加载和保存记录集或流时检查
 ADO 2.7 和更早版本中，为文件输入/输出操作如[开放](../../ado/reference/ado-api/open-method-ado-recordset.md)并[保存](../../ado/reference/ado-api/save-method.md)使用的读取和写入基于文件的数据可能在某些情况下允许的 URL 或文件名称用于指定非磁盘基于文件类型。 例如，LPT1，COM2，PRN。TXT、 AUX 无法用作别名之间打印机上的和辅助设备系统使用特定的输入/输出

 ADO 2.8 和更高版本中，为已更新此功能。 用于打开和保存**记录集**并**Stream**对象，ADO 现在执行文件类型检查，以确保 URL 或文件名称中指定的输入或输出设备的实际文件。

> [!NOTE]
>  文件类型检查在本部分中所述仅适用于 Windows 2000 及更高版本。 它不适用于 ADO 2.8 或更高版本在早期 Windows 版本中，例如 Windows 98 的运行位置的情况下。
