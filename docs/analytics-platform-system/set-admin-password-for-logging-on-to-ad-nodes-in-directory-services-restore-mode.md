---
title: "在目录服务还原模式 (AP) 中设置 AD 节点管理员登录密码"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97a9c715-2763-417d-b45c-bb0180759e47
caps.latest.revision: "20"
ms.openlocfilehash: 2e0379093db9364f45793adc20635bfa4ad53748
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm"></a>在目录服务还原模式 (DSRM) 中设置管理员密码用于登录到 AD 节点
目录服务还原模式 (DSRM) 是一种用于修复或恢复 Active Directory 域服务 (AD DS) 的启动模式。 它用于 AD DS 发生故障后或在 AD DS 需要还原时登录到设备 AD 节点。 为 DSRM 密码硬件供应商站点上的设备安装过程已初始化，并且应由设备管理员更改。 分析平台系统具有两个 AD DS （域控制器）; ***appliance_domain*-AD01**和 ***appliance_domain*-AD02**。 对于每个设备 AD 节点，请更改使用以下步骤的 DSRM 密码。  
  
## <a name="HowToDSRM"></a>若要重置管理员密码  
  
1.  打开命令提示符窗口的设备 AD 节点上  ***appliance_domain*– AD*xx** * 虚拟机。  
  
2.  在命令提示符处，键入`ntdsutil`。  
  
3.  在**ntdsutil**提示符下，键入`set dsrm password`。  
  
4.  在**重置管理员密码：**提示符下，键入`reset password on server null`。  
  
5.  在提示符处，键入新密码。  
  
6.  对每个设备 AD 虚拟机重复步骤 1 到 5 之上。  
  
    > [!WARNING]  
    > 分析平台系统不支持美元符号 （$） 中的域管理员或本地管理员密码。 包含美元符号的密码将验证并可使用、 但可能会阻止升级和维护活动。  
  
> [!NOTE]  
> 如果 Active Directory 域服务或虚拟机将成为损坏的特定 AD 虚拟机中，运行**ReplaceVM**受影响 ad 虚拟机是建议的纠正操作。 以获取帮助的联系 CSS。  
  
## <a name="see-also"></a>另请参阅  
[密码重置 &#40;分析平台系统 &#41;](password-reset.md)  
  
