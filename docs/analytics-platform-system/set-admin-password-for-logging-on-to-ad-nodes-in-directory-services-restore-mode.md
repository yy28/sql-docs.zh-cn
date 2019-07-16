---
title: 设置 Active Directory 密码的分析平台系统 |Microsoft Docs
description: 在目录服务还原模式中 Analytics Platform System (APS) 中设置 Active Directory 节点管理员登录密码。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3e0b197a044f2f008b886d5f2ff39b603821fd29
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960067"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>设置管理员密码登录到 AD 节点在目录服务还原模式 (DSRM) 中的分析平台系统
目录服务还原模式 (DSRM) 是用于修复或恢复 Active Directory 域服务 (AD DS) 的启动模式。 它用于登录到设备 AD 节点后未通过 AD DS 或 AD DS 需要还原。 为 DSRM 密码在硬件供应商站点上设备安装过程已初始化，应更改设备管理员。 分析平台系统具有两个 AD DS （域控制器）; **_appliance_domain_-AD01**并 **_appliance_domain_-AD02**。 对于每个设备 AD 节点，使用以下步骤将 DSRM 密码的更改。  
  
## <a name="HowToDSRM"></a>若要重置管理员密码  
  
1.  打开设备 AD 节点上的命令提示符窗口 <strong>_appliance_domain_-AD_xx_</strong>虚拟机。  
  
2.  在命令提示符下键入 `ntdsutil`。  
  
3.  在**ntdsutil**提示符下，键入`set dsrm password`。  
  
4.  在**重置管理员密码：** 提示符下，键入`reset password on server null`。  
  
5.  在提示符处，键入新密码。  
  
6.  对每个设备 AD 虚拟机重复步骤 1-5 上面。  
  
    > [!WARNING]  
    > 分析平台系统不支持在域管理员或本地管理员密码的美元符号 （$）。 包含美元符号的密码将验证并将可用，但可能会阻止升级和维护活动。  
  
> [!NOTE]  
> 如果 Active Directory 域服务或虚拟机损坏的特定 AD 虚拟机，运行**将**为受影响 AD 虚拟机是建议的纠正操作。 请与 CSS 联系以获得帮助。  
  
## <a name="see-also"></a>请参阅  
[密码重置&#40;分析平台系统&#41;](password-reset.md)  
  
