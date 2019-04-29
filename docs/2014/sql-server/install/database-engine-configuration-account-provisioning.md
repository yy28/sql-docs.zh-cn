---
title: 数据库引擎配置-帐户设置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 834b26bc-49de-4033-88d5-6aa7b1609720
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69885ad9affb87ea160231fa6f6d42d0fef7ea6c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62987924"
---
# <a name="database-engine-configuration---account-provisioning"></a>数据库引擎配置 - 帐户设置
  使用此页可以设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全模式，并添加 Windows 用户或组作为 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的管理员。  
  
## <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>有关运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的注意事项  
 在以前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，将 **BUILTIN\Administrators** 组设置为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中的登录名，本地 Administrators 组的成员可以使用其管理员凭据登录。 使用提升的权限并不是最好的做法。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，未将 **BUILTIN\Administrators** 组设置为登录名。 因此，您应为每个管理用户创建一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，并在安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]新实例的过程中将该登录名添加到 sysadmin 固定服务器角色中。 对于用来运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的 Windows 帐户，您也应该执行这些操作。 这些作业包括复制代理作业。  
  
## <a name="options"></a>选项  
 **安全模式** - 选择“Windows 身份验证”或“混合模式身份验证”用于安装。  
  
 **Windows 主体设置** - 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的早期版本中，Windows Builtin\Administrator 本地组放入了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin 服务器角色中，有效授予了 Windows 管理员对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的访问权限。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的 sysadmin 服务器角色中未设置 Builtin\Administrator 组， 而是改为由您在安装过程中为新安装显式设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员。  
  
> [!IMPORTANT]  
>  您在安装过程中必须为新安装显式设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员。 直到您完成此步骤之后，安装程序才允许您继续操作。  
  
 **指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员** - 必须为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例至少指定一个 Windows 主体。 若要添加用以运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的帐户，请单击 **“当前用户”** 按钮。 若要向系统管理员列表中添加帐户或从中删除帐户，请单击 **“添加”** 或 **“删除”**，然后编辑将拥有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的管理员权限的用户、组或计算机的列表。  
  
 完成列表的编辑后，单击 **“确定”**，然后在配置对话框中验证管理员列表。 完成此列表后，请单击 **“下一步”**。  
  
 如果选择“混合模式身份验证”，则必须为内置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员 (SA) 帐户提供登录凭据。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Windows 身份验证模式**  
 当用户通过 Windows 用户帐户连接时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用操作系统中的 Windows 主体标记验证帐户名和密码。 此为默认身份验证模式，比混合模式更为安全。 Windows 身份验证利用 Kerberos 安全协议，通过强密码的复杂性验证提供密码策略强制，提供帐户锁定支持，并且支持密码过期。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]切勿设置空密码或弱 sa 密码。  
  
 **混合模式（Windows 身份验证或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证）**  
 允许用户使用 Windows 身份验证或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接。 通过 Windows 用户帐户进行连接的用户可以使用经过 Windows 验证的可信连接。  
  
 如果必须选择“混合模式身份验证”并且要求使用 SQL 登录名以适应早期应用程序，则必须为所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户设置强密码。  
  
> [!NOTE]  
>  提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证只是为了向后兼容。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **输入密码**  
 输入并确认系统管理员 (sa) 登录名。 密码是抵御入侵者的第一道防线，因此设置强密码对于系统安全是绝对必要的。 切勿设置空密码或弱 sa 密码。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密码可包含 1 到 128 个字符，包括字母、符号和数字的任意组合。 如果选择“混合模式身份验证”，则必须输入强 sa 密码才能进入安装向导的下一页。  
  
 **强密码指南**  
 强密码不易被人猜出，也不易用计算机程序攻击。 强密码不能使用禁止的条件或字词，这些条件或字词包括：  
  
-   空条件或 NULL 条件  
  
-   “Password”  
  
-   “Admin”  
  
-   “Administrator”  
  
-   “sa”  
  
-   “sysadmin”  
  
 强密码不能是与安装计算机相关联的下列字词：  
  
-   当前登录到计算机的用户的名称。  
  
-   计算机名称。  
  
 强密码的长度必须多于 8 个字符，并且强密码至少要满足下列四个条件中的三个：  
  
-   它必须包含大写字母。  
  
-   它必须包含小写字母。  
  
-   必须包含数字。  
  
-   必须包含非字母数字字符；例如 #、% 或 ^。  
  
 此页上输入的密码必须符合强密码策略要求。 如果存在任何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的自动化过程，请确保该密码符合强密码策略要求。  
  
## <a name="related-content"></a>相关内容  
 有关选择 Windows 身份验证和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“选择身份验证模式”主题。  
  
 有关选择帐户以运行 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的详细信息，请参阅 **联机丛书中的“配置 Windows 服务帐户和权限”**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主题。  
  
## <a name="see-also"></a>请参阅  
 [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
