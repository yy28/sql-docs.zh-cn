---
title: 密码重置
description: 密码重置页面使你可以更改分析平台系统所使用的管理员帐户的密码。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 952dbda04b4f7132406e3a6de4479afea1be92e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400905"
---
# <a name="password-reset---analytics-platform-system"></a>密码重置-分析平台系统
**密码重置**页面使你可以更改分析平台系统所使用的管理员帐户的密码。  
  
> [!WARNING]  
> 始终使用**Configuration Manager**来更新设备的域管理员密码。 其他方法可能不会更新分析平台系统的所有组件，可能会导致设备访问问题。  
  
交付设备后，系统会向你提供分析平台系统密码。 当你承担设备责任时，请始终将密码更改为新值。 有三个要更新的密码。 密码不必与其他密码相同。  
  
**F<*xxxx*> \administrator**  
设备域的**管理员**。  
  
**.\Administrator**  
承载虚拟机的计算机上的本地**管理员**帐户。  
  
> [!IMPORTANT]  
> 对于 "设备更新 1"， **Configuration Manager**不会在 PDW VM 的整个中正确更改本地管理员帐户的密码。 如果需要，请联系 CSS 以获取其他说明。  
  
**成为**  
SQL Server 中的**sa**登录名。 **sa**是**sysadmin**固定服务器角色的成员，是 SQL Server 管理员。 还可以使用**ALTER login**语句更改**sa**登录名的密码。  
  
## <a name="password-requirements"></a>密码要求  
域管理员凭据和系统管理员凭据都遵循每种类型的凭据的密码强度策略。 更改域管理员凭据时，新密码会在 SQL Server PDW 所需的位置更新为域。  
  
> [!IMPORTANT]  
> SQL Server PDW 不支持域管理员或本地管理员密码**$** 中的美元符号字符（）。 密码 **^% &** 允许使用密码，但 PowerShell 将这些字符视为特殊字符。 如果在系统管理员或 SQL Server**sa**帐户的密码中使用了这些字符中的任何一个（在安装过程中， **AdminPassword**和**PdwSAPassword**参数），安装程序（包括安装、升级、REPLACENODE 和修补）都将失败。 若要确保在当前密码包含不受支持的字符时成功升级，请更改这些密码，使其在运行升级之前不包含这些字符。 升级完成后，可以将这些密码设置回其原始值。 有关密码要求的详细信息，请参阅[ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)。  
  
## <a name="to-reset-a-password"></a>重置密码  
  
1.  连接到控件节点并启动**Configuration Manager** （**dwconfig**）。 有关详细信息，请参阅[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)。  
  
2.  在**Configuration Manager**的左窗格中，单击 "**密码重置**"。  
  
3.  从 "**帐户**" 下拉菜单中选择 "管理员" 类型，然后在 "**密码**" 和 "**确认密码**" 框中输入新密码。 单击 "**应用**" 以保存所做的更改。  
  
    对这些帐户所做的更改不会影响任何当前处于活动状态的会话，但会在每个用户下次登录尝试时应用。  
  
    ![SQL Server DWConfig 密码](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>另请参阅  
[在目录服务还原模式下，为登录 AD 节点设置管理员密码 &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)  
  
