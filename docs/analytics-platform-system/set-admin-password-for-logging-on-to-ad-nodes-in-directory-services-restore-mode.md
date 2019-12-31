---
title: 设置 Active Directory 密码
description: 在分析平台系统（AP）中，设置目录服务还原模式下 Active Directory 节点的管理员登录密码。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbbf42106602a25b03072a9c9abfb04f04d3c49
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400335"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>为在目录服务还原模式（DSRM）分析平台系统中登录 AD 节点设置管理员密码
目录服务还原模式（DSRM）是一种用于修复或恢复 Active Directory 域服务（AD DS）的启动模式。 它用于在 AD DS 失败或需要还原 AD DS 后登录到设备 AD 节点。 DSRM 的密码已在硬件供应商站点的设备设置过程中初始化，应由设备管理员更改。 分析平台系统有两个 AD DS （域控制器）;** _appliance_domain_-AD01**和** _appliance_domain_-AD02**。 对于每个设备 AD 节点，请使用以下步骤更改 DSRM 密码。  
  
## <a name="HowToDSRM"></a>重置管理员密码  
  
1.  在设备 AD 节点<strong> _appliance_domain_AD_xx_</strong>虚拟机上打开命令提示符窗口。  
  
2.  在命令提示符处，键入：`ntdsutil`。  
  
3.  在**ntdsutil**提示符下，键入`set dsrm password`。  
  
4.  在 "**重置管理员密码：** " 提示符`reset password on server null`下，键入。  
  
5.  在提示符下，键入新密码。  
  
6.  为每个设备 AD 虚拟机重复上述步骤 1-5。  
  
    > [!WARNING]  
    > 分析平台系统不支持域管理员或本地管理员密码中的美元符号字符（$）。 包含美元符号的密码将验证并且可用，但会阻止升级和维护活动。  
  
> [!NOTE]  
> 如果 Active Directory 域服务或虚拟机对于特定 AD 虚拟机已损坏，则建议对受影响的 AD 虚拟机运行**ReplaceVM** 。 若要获取帮助，请联系 CSS。  
  
## <a name="see-also"></a>另请参阅  
[&#40;分析平台系统&#41;的密码重置](password-reset.md)  
  
