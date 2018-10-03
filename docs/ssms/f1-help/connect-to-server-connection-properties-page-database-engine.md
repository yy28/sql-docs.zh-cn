---
title: 连接到服务器（“连接属性”页）（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connecttoce.connectionproperties.f1
- sql13.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 890729b400328edaa8a0bdb8904ee7c0b64f2482
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47797403"
---
# <a name="connect-to-server-connection-properties-page-database-engine"></a>连接到服务器（“连接属性”页）（数据库引擎）
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
使用此选项卡可在连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] 实例或在“已注册的服务器”中注册 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 时查看或指定选项。 只有在连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 实例时，此对话框中才显示“连接”和“选项”。 注册 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 时，此对话框中仅显示“测试”和“保存”。  
  
**连接到数据库**  
从列表中选择要连接到的数据库。 如果选择“<default>”，则将连接到服务器的默认数据库。 如果选择 **<Browse server>**，则可以浏览要连接的数据库的服务器。  
  
在通过 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎的一个实例时，必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，并且必须在“连接到服务器”对话框的“连接属性”选项卡上指定一个数据库。请确保选中“加密连接”复选框。  
  
默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将连接到 **master**。 连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 时，如果指定用户数据库，则对象资源管理器中仅显示该数据库及其对象。 如果连接到 master，则会显示所有数据库。 有关详细信息，请参阅 [Windows Azure SQL 数据库概述](http://go.microsoft.com/fwlink/?LinkId=163948)。  
  
**网络协议**  
从该列表中选择某个协议。 可用客户端协议是你通过“计算机管理”中的“客户端网络配置”配置的协议。  
  
**网络数据包大小**  
输入要发送的网络数据包的大小。 默认值为 4096 字节。  
  
**连接超时值**  
输入在超时之前等待建立连接的秒数。默认值为 15 秒。  
  
**执行超时值**  
输入在服务器上完成任务执行之前等待的时间（秒）。 默认值为零秒，指示无超时。  
  
**加密连接**  
强制对连接进行加密。  
  
**使用自定义颜色**  
选择此选项可以指定 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 查询编辑器窗口中状态栏的背景颜色。 若要指定颜色，请单击“选择”。 在“颜色”对话框中，从“基本颜色”网格中选择一种预定义颜色，或者单击“定义自定义颜色”定义并使用自定义颜色。  
  
-   如果在“对象资源管理器”窗格中指定了服务器条目的颜色，则在打开查询编辑器窗口时将使用此颜色。 若要打开查询编辑器窗口，可以右键单击服务器条目，然后选择“新建查询”，或者如果“对象资源管理器”窗格处于活动状态且其焦点位于此服务器上，则可以单击工具栏上的“新建查询”。  
  
-   如果在“已注册的服务器”窗格中指定了服务器条目的颜色，则在打开查询编辑器窗口时将使用此颜色。 若要打开查询编辑器窗口，可以右键单击服务器条目，然后选择“新建查询”，或者如果“已注册的服务器”窗格处于活动状态且其焦点位于此服务器上，则可以单击工具栏上的“新建查询”。  
  
-   依次单击“文件”菜单上的“新建”和“数据库引擎查询”后，在“连接到服务器”对话框中指定的颜色即应用于此查询编辑器窗口。  
  
**AD 域名或租户 ID**  
通过“Active Directory - 含 MFA 支持的通用身份验证”连接时，请指定身份验证的域。 仅当使用 SSMS 17.2 或更高版本时，此选项才可用。 

**全部重置**  
将所有手动输入的连接属性值替换为默认值。  
  
**“连接”**  
使用列出的值尝试连接。  
  
**选项**  
单击此选项更改对话框并隐藏其他服务器连接选项，例如记住密码。  
  
**测试**  
在“已注册的服务器”中注册 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 时，单击此选项可以测试连接。  
  
**保存**  
保存“已注册的服务器”中的设置。  
  
## <a name="see-also"></a>另请参阅  
[“连接属性”对话框](../../ssms/f1-help/connection-properties-dialog-box.md)  
  
