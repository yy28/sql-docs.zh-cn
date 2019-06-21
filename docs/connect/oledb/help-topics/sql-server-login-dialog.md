---
title: SQL Server 登录对话框 (OLE DB) |Microsoft Docs
description: 使用 SQL Server 登录对话框
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: 4735ead33dc7c3a6d633e3b23ff1da97eeae4962
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62853270"
---
# <a name="sql-server-login-dialog-box"></a>SQL Server 登录对话框
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

当你尝试连接而无需指定足够的信息时，OLE DB 驱动程序将显示**SQL Server 登录名**对话框。

> [!NOTE]  
> SQL Server 登录对话框，提示行为由控制`DBPROP_INIT_PROMPT`初始化属性。 有关详细信息，请参阅：
> - [初始化和授权属性](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [OLE DB 程序员指南](https://go.microsoft.com/fwlink/?linkid=2067702)

![SQL Server 登录名对话框的屏幕截图](../media/sql-server-login-dialog.png)

## <a name="options"></a>选项
|选项|描述|
|---   |---        |
|“服务器”|在网络上的 SQL Server 实例的名称。 从列表中选择一个服务器\实例名，或在“服务器”  框中键入服务器\实例名。 或者，可以在客户端计算机上使用“SQL Server 配置管理器”  创建服务器别名，并在“服务器”  框中键入该名称。 <br/><br/>当使用与 SQL Server 相同的计算机时可以输入“(local)”。 即使正在运行非联网版的 SQL Server，也可以连接到 SQL Server 的本地实例。<br/><br/>有关不同类型的网络的服务器名称的详细信息，请参阅[SQL Server 安装](https://go.microsoft.com/fwlink/?linkid=2067541)。|
|身份验证模式|您可以从下拉列表中选择以下身份验证选项：<br/><ul><li>`Windows Authentication:` 对使用当前登录的用户的 Windows 帐户凭据的 SQL Server 身份验证。</li><li>`SQL Server Authentication:` 对使用登录 ID 和密码的 SQL Server 身份验证。</li><li>`Active Directory - Integrated:` 使用当前登录的用户的 Windows 帐户凭据的集成身份验证。</li><li>`Active Directory - Password:` Active Directory 身份验证使用登录 ID 和密码。</li></ul>|
|服务器 SPN|如果您使用受信任连接，则可为服务器指定服务主体名称 (SPN)。|
|登录 ID|指定要用于连接的登录名 ID。 仅启用了登录 ID 文本框中，如果`Authentication Mode`设置为`SQL Server Authentication`或`Active Directory - Password`。|
|Password|指定用于连接的密码。 仅已启用密码文本框中，如果`Authentication Mode`设置为`SQL Server Authentication`或`Active Directory - Password`。|
|选项|显示或隐藏“选项”  组。 如果“服务器”具有值，则启用“选项”   按钮。|
|更改密码|选中此选项，使**新密码**并**确认新密码**文本框。|
|新密码|指定新密码。|
|确认新密码|再次指定新密码以便确认。|
|“数据库”|选择或键入将用于该连接的默认数据库。 此设置将覆盖为该服务器上的登录名指定的默认数据库。 如果未指定数据库，连接将使用为该服务器上的登录名指定的默认数据库。|
|镜像服务器|指定要镜像的数据库的故障转移伙伴的名称。|
|镜像 SPN|您还可以指定镜像服务器的 SPN。 镜像服务器的 SPN 用于在客户端和服务器之间相互进行身份验证。|
|“报表”|指定用于 SQL Server 系统消息的国家/地区语言。 运行 SQL Server 的计算机必须安装该语言。 此设置将覆盖为该服务器上的登录名指定的默认语言。 如果未指定语言，连接将使用为该服务器上的登录名指定的默认语言。|
|应用程序名称|指定将要存储在 sys.sysprocesses  中该连接所在行的 program_name  列中的应用程序名称。|
|工作站 ID|指定将要存储在 sys.sysprocesses  中该连接所在行的 hostname  列中的工作站 ID。|
|对数据使用强加密|选择它时，将加密数据，通过连接进行传递。|
|信任服务器证书|选中后，将验证服务器的证书。 服务器的证书必须具有正确的主机名的服务器和受信任的证书颁发机构颁发。|

> [!NOTE]  
> 使用时`Windows Authentication`或`SQL Server Authentication`模式下，**信任服务器证书**被视为仅当**对数据使用强加密**选项处于启用状态。

## <a name="next-steps"></a>后续步骤
- [向 Azure Active Directory 进行身份验证](../features/using-azure-active-directory.md)使用 OLE DB 驱动程序。
- 使用组连接信息[通用数据链接 (UDL)](data-link-pages.md)。