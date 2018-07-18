---
title: 设置分析平台系统的 Active Directory 密码-|Microsoft 文档
description: 在目录服务还原模式中分析平台系统 (AP) 中设置 Active Directory 节点管理员登录密码。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e74689216c1485fc0c11c588acb151269e2b5d2b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538377"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>设置管理员密码登录到 AD 节点在目录服务还原模式 (DSRM)-分析平台系统
目录服务还原模式 (DSRM) 是一种用于修复或恢复 Active Directory 域服务 (AD DS) 的启动模式。 它用于 AD DS 发生故障后或在 AD DS 需要还原时登录到设备 AD 节点。 为 DSRM 密码硬件供应商站点上的设备安装过程已初始化，并且应由设备管理员更改。 分析平台系统具有两个 AD DS （域控制器）;***appliance_domain *-AD01**和 ***appliance_domain *-AD02**。 对于每个设备 AD 节点，请更改使用以下步骤的 DSRM 密码。  
  
## <a name="HowToDSRM"></a>若要重置管理员密码  
  
1.  打开命令提示符窗口的设备 AD 节点上***appliance_domain *– AD*xx***虚拟机。  
  
2.  在命令提示符处，键入`ntdsutil`。  
  
3.  在**ntdsutil**提示符下，键入`set dsrm password`。  
  
4.  在**重置管理员密码：** 提示符下，键入`reset password on server null`。  
  
5.  在提示符处，键入新密码。  
  
6.  对每个设备 AD 虚拟机重复步骤 1 到 5 之上。  
  
    > [!WARNING]  
    > 分析平台系统不支持美元符号 （$） 中的域管理员或本地管理员密码。 包含美元符号的密码将验证并可使用、 但可能会阻止升级和维护活动。  
  
> [!NOTE]  
> 如果 Active Directory 域服务或虚拟机将成为损坏的特定 AD 虚拟机中，运行**ReplaceVM**受影响 ad 虚拟机是建议的纠正操作。 以获取帮助的联系 CSS。  
  
## <a name="see-also"></a>另请参阅  
[密码重置&#40;分析平台系统&#41;](password-reset.md)  
  
