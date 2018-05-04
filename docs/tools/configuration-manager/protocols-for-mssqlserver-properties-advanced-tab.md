---
title: MSSQLSERVER 属性的协议（“高级”选项卡）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: abd5ca68-825f-4c07-b27c-3b3a79d03d74
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67d9b33fd5326a3f0195acf0987215d6689d1fb3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="protocols-for-mssqlserver-properties-advanced-tab"></a>MSSQLSERVER 属性的协议（“高级”选项卡）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  使用 **“MSSQLSERVER 属性的协议”** 对话框上的 **“高级”** 选项卡为   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]。 **扩展保护** 是操作系统实现的一项网络组件功能。 Windows 7 和 Windows Server 2008 R2 提供**扩展保护** ，旧操作系统的 Service Pack 中也包括此功能。 使用**扩展保护**进行连接时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会更安全。 **扩展保护** 功能的一些好处需要选定 **“标志”** 选项卡上的 **“强行加密”** 后才能获得。  
  
> [!IMPORTANT]  
>  默认情况下，Windows 不启用 **扩展保护** 。 有关如何在 Windows 中启用 **扩展保护** 的信息，请参阅知识库文章 [针对验证的扩展保护](http://go.microsoft.com/fwlink/?LinkId=178431)。  
  
 有关如何配置其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务，以及 **扩展保护**的完整描述，请参阅 [Microsoft.com](http://go.microsoft.com/fwlink/?LinkId=177752)上的最新信息。  
  
 从 开始的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 完全支持扩展保护 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。 目前不支持将 **扩展保护** 用于其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端提供程序。  
  
## <a name="options"></a>“常规”  
 **扩展保护**  
 有三种可能的值：  
  
-   当设置为 **“关闭”**时，禁用 **扩展保护** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例将接受来自任何客户端的连接，不管该客户端是否受保护。 “关闭” 选项虽与旧的和未打补丁的操作系统兼容，但安全性较差。 只有在您知道客户端操作系统不支持扩展保护的情况下才使用此设置。  
  
-   当设置为 **“允许”**时，来自支持 **扩展保护** 的操作系统的连接需要 **扩展保护**。 来自运行在受保护客户端操作系统上的不受保护客户端应用程序的连接被拒绝。 对于来自不受保护操作系统的连接，忽略**扩展保护** 。 此设置虽比 **“关闭”**更安全，但仍不是最安全的设置。 在混合环境（即有些操作系统或应用程序支持 **扩展保护** ，有些不支持）中使用此设置。  
  
-   当设置为 **“必需”**时，只接受来自受保护操作系统上受保护应用程序的连接。 此设置在三个选项中是最安全的，但来自不支持 **扩展保护** 的操作系统的连接将无法连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 **接受的 NTLM SPN**  
 当多个 NTLM 服务主体名称 (SPN) 标识 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例时，在此以字符串系列形式列出 SPN，字符串之间用分号分隔。 例如，值 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com**指示允许客户端尝试连接到名为 **MSSQLSvc/HOST1.Contoso.com** 和 **MSSQLSvc/HOST2.Contoso.com** 的 SPN。 变量的最大长度为 2048 个字符。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 针对验证的扩展保护](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)  
  
  
