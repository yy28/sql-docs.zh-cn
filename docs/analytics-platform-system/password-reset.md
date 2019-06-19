---
title: 密码重置-分析平台系统 |Microsoft Docs
description: 密码重置页，可更改使用的分析平台系统的管理员帐户的密码。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 63fbb097bf1ca926223ce7c0114c8da5d10cd969
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639952"
---
# <a name="password-reset---analytics-platform-system"></a>密码重置-分析平台系统
**密码重置**页使你可以更改使用的分析平台系统的管理员帐户的密码。  
  
> [!WARNING]  
> 始终使用**Configuration Manager**来更新设备域管理员密码。 其他方法可能不会更新分析平台系统的所有组件，并可能导致设备访问权限问题。  
  
传递设备时，你可以分析平台系统密码。 始终为新值更改的密码，你可以将设备时。 有三个密码更新。 密码无需为彼此相同。  
  
**F<*xxxx*>\Administrator**  
**管理员**的设备域。  
  
**.\Administrator**  
本地**管理员**上托管的虚拟机的计算机帐户。  
  
> [!IMPORTANT]  
> 设备的更新 1， **Configuration Manager**不能完全更改整个 PDW VM 的本地管理员帐户的密码。 如果这是有必要，请联系 CSS 的更多说明。  
  
**sa**  
**Sa**中 SQL Server 登录名。 **sa**隶属**sysadmin**固定服务器角色，并且是 SQL Server 管理员。 密码**sa**还可以通过更改登录名**ALTER LOGIN**语句。  
  
## <a name="password-requirements"></a>密码要求  
域管理员凭据和系统管理员凭据遵循每种类型的凭据的密码强度策略。 新密码时更改域管理员凭据，将更新到域在需要时在 SQL Server PDW。  
  
> [!IMPORTANT]  
> SQL Server PDW 不支持将美元符号 ( **$** ) 中的域管理员或本地管理员密码。 字符 **^ %&** 允许密码，但 PowerShell 将这些作为特殊字符。 如果系统管理员或 SQL Server 使用在密码中任何这些字符**sa**帐户 ( **AdminPassword**并**PdwSAPassword**期间的参数安装程序） 设置，包括安装、 升级、 REPLACENODE 和修补，将会失败。 若要确保成功升级当前的密码包含不支持的字符时，更改这些密码，以便它们运行升级之前，不包含此类字符。 升级完成后，可以将这些密码设置回其原始值。 有关密码要求的详细信息，请参阅[ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)。  
  
## <a name="to-reset-a-password"></a>若要重置密码  
  
1.  连接到控制节点并启动**Configuration Manager** (**dwconfig.exe**)。 有关详细信息，请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在左窗格中**Configuration Manager**，单击**密码重置**。  
  
3.  选择管理员类型从**帐户**下拉列表菜单，然后输入中的新密码**密码**并**确认密码**框。 单击**应用**以保存所做的更改。  
  
    对这些帐户所做的更改不会影响任何当前处于活动状态的会话，但将在每个用户下次登录应用。  
  
    ![SQL Server DWConfig 密码](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>请参阅  
[在目录服务还原模式中设置管理员密码用于登录到 AD 节点&#40;DSRM&#41; &#40;分析平台系统&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[启动配置管理器&#40;分析平台系统&#41;](launch-the-configuration-manager.md)  
  
