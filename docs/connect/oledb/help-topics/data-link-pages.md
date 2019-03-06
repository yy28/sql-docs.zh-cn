---
title: 通用数据链接 (UDL) 配置 |Microsoft Docs
description: 使用用于 SQL Server 的 Microsoft OLE DB 驱动程序的通用数据链接 (UDL) 配置
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: e198f561fd4f6bcec390ef8632c1cdc96f2810d6
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744796"
---
# <a name="universal-data-link-udl-configuration"></a>通用数据链接 (UDL) 配置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>“连接”选项卡
使用连接选项卡来指定如何连接到使用 Microsoft OLE DB 驱动程序适用于 SQL Server 数据。

![OLE DB 数据链接页-连接选项卡的屏幕截图](../media/data-link-pages-connection-tab.png)

该“连接”选项卡特定于提供程序并且只显示适用于 SQL Server 的 Microsoft OLE DB 驱动程序需要的连接属性。

|选项|描述|
|---   |---        |
|选择或输入服务器名称|从下拉列表中选择服务器名称，或者键入要访问的数据库所在的服务器的位置。 在服务器上选择数据库是一项单独的操作。 单击“刷新”可更新列表。
|输入登录到服务器的信息|您可以从此下拉列表中选择以下身份验证选项： <ul><li>`Windows Authentication:` 对使用当前登录的用户的 Windows 帐户凭据的 SQL Server 身份验证。</li><li>`SQL Server Authentication:` 对使用登录 ID 和密码的 SQL Server 身份验证。</li><li>`Active Directory - Integrated:` 使用当前登录的用户的 Windows 帐户凭据的集成身份验证。</li><li>`Active Directory - Password:` Active Directory 身份验证使用登录 ID 和密码。</li></ul>|
|服务器 SPN|如果您使用受信任连接，则可为服务器指定服务主体名称 (SPN)。|
|“用户名”|键入要在登录到数据源时用于身份验证的用户 ID。|
|Password|键入要用于身份验证，当你登录到数据源的密码。|
|空密码|选中此选项，使指定的提供程序连接字符串中使用空密码。|
|允许保存密码|选中时，允许以与连接字符串一起保存的密码。 是否在连接字符串中包括密码取决于调用应用程序的功能。 <br/><br/>注意：如果保存密码，则密码在返回和保存时是未屏蔽和未加密的。|
|对数据使用强加密|选择它时，将加密数据，通过连接进行传递。|
|信任服务器证书|选中后，将验证服务器的证书。 服务器的证书必须具有正确的主机名的服务器和受信任的证书颁发机构颁发。|
|选择数据库|选择或键入你想要访问的数据库名称。|
|附加数据库文件作为数据库名称|指定可附加数据库的主文件的名称。 该数据库作为数据源的默认数据库附加和使用。 在此节下第一个文本框中，键入要附加的数据库文件使用的数据库名称。<br/><br/>键入要在文本框中标记为附加的数据库文件的完整路径`Using the filename`，或单击`...`按钮以浏览数据库文件。|
|更改密码|显示更改 SQL Server 密码对话框。 |
|“测试连接”|单击此项可尝试连接到指定的数据源。 如果连接失败，请确保设置是正确的。 例如，拼写错误和大小写不同均可能导致连接失败。|

## <a name="advanced-tab"></a>高级选项卡
使用高级选项卡来查看和设置附加的初始化属性。

![OLE DB 数据链接页-高级选项卡的屏幕截图](../media/data-link-pages-advanced-tab.png)

|选项|描述|
|---   |---        |
| 连接超时 | 指定 （以秒为单位） 的 Microsoft OLE DB Driver for SQL Server 等待初始化完成的时间量。 如果初始化超时，则返回一个错误并且不创建该连接。|


> [!NOTE]  
>  有关更多常规链接列出的数据连接信息，请参阅[数据链接 API 概述](https://go.microsoft.com/fwlink/?linkid=2067432)。

## <a name="next-steps"></a>后续步骤
- [向 Azure Active Directory 进行身份验证](../features/using-azure-active-directory.md)使用 OLE DB 驱动程序。

- [提示用户进行身份验证凭据](../help-topics/sql-server-login-dialog.md)使用 OLE DB 驱动程序。