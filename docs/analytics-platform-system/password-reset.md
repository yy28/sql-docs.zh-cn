---
title: "密码重置 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0f808fc-e120-430b-b6c9-11f2b1c90bf3
caps.latest.revision: "26"
ms.openlocfilehash: 260e7ad5adc45cb19458e36d15f6f35345ea0d2c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="password-reset"></a>密码重置
**密码重置**页使你可以更改由分析平台系统使用的管理员帐户的密码。  
  
> [!WARNING]  
> 始终使用**Configuration Manager**更新设备域管理员密码。 其他方法可能不会更新分析平台系统的所有组件，并且可能会导致设备访问权限问题。  
  
传递设备时，你可以分析平台系统密码。 当你拍摄负责你的设备时始终为新值更改的密码。 有三个密码更新。 密码不需要为每个其他相同。  
  
**F <*xxxx*> \Administrator**  
**管理员**的设备域。  
  
**。 \Administrator**  
本地**管理员**上托管的虚拟机的计算机帐户。  
  
> [!IMPORTANT]  
> 对于设备更新 1， **Configuration Manager**不能完全更改整个 PDW VM 的本地管理员帐户的密码。 如果需要，请联系 CSS 的更多说明。  
  
**sa**  
**Sa**中 SQL Server 登录名。 **sa**为属于**sysadmin**固定服务器角色，并且是 SQL Server 管理员。 密码**sa**还可以通过使用更改登录**ALTER LOGIN**语句。  
  
## <a name="password-requirements"></a>密码要求  
域管理员凭据和系统管理员凭据遵守每种类型的凭据的密码强度策略。 新密码时更改域管理员凭据，将更新到域在整个 SQL Server PDW 需要的地方。  
  
> [!IMPORTANT]  
> SQL Server PDW 不支持的美元符号字符 (**$**) 中的域管理员或本地管理员密码。 字符**^ %&**允许密码，但是 PowerShell 将这些作为特殊字符。 如果任何这些字符用于在密码中的系统管理员或 SQL Server**sa**帐户 ( **AdminPassword**和**PdwSAPassword**期间的参数安装程序） 然后安装程序，包括安装、 升级、 REPLACENODE 和修补，将会失败。 若要在当前的密码包含不支持的字符时，请确保成功升级，请更改这些密码，以便它们在运行升级之前不包含此类字符。 升级完成后，你可以将这些密码设置回其原始值。 有关密码要求的详细信息，请参阅[ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)。  
  
## <a name="to-reset-a-password"></a>若要重置密码  
  
1.  连接到控制节点并启动**Configuration Manager** (**dwconfig.exe**)。 有关详细信息，请参阅[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md).  
  
2.  在左窗格中**Configuration Manager**，单击**密码重置**。  
  
3.  选择管理员类型从**帐户**下拉列表菜单，然后输入中的新密码**密码**和**确认密码**框。 单击**应用**以保存所做的更改。  
  
    对这些帐户所做的更改不会影响任何当前处于活动状态的会话，但将在每个用户下一次登录尝试应用。  
  
    ![SQL Server DWConfig 密码](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>另请参阅  
[设置管理员密码用于登录到 AD 节点在目录服务还原模式 &#40; DSRM &#41;&#40;分析平台系统 &#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md)  
  
