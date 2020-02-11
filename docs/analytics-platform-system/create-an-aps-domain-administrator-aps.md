---
title: 创建域管理员
description: 某些操作需要分析平台系统域管理员特权。 这说明了如何创建其他设备管理员。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1a0d50e485f0e8f48de11b2e5a3c27c9f9be047e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401235"
---
# <a name="create-an-aps-domain-administrator"></a>创建 AP 域管理员
某些操作需要分析平台系统域管理员特权。 这说明了如何创建其他设备管理员。  
  
## <a name="create-a-domain-administrator"></a>创建域管理员  
要拥有足够的权限来配置所有的 ap 节点，运行**ap Configuration Manager** （`dwconfig.exe`）的用户必须是**Domain Admins**组的成员。 若要启动和停止 AP 服务，用户必须是**PdwControlNodeAccess**组的成员。  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>将用户添加到域管理员组  
  
1.  使用现有的设备域管理员帐户登录到活动 AD 节点 **（_设备\_域_-AD01**或**_设备\_域_-AD02**）。  
  
2.  在 “开始” 菜单上，单击 **“运行”** 。 在 "**打开**" 框中，键入**dsa.msc**。 单击“确定”。   
  
3.  在**Active Directory 用户和计算机**"程序中，右键单击 **" 用户**"，指向"**新建**"，然后单击"**用户**"。  
  
4.  在 "**新建对象-用户**" 对话框中，完成新用户的说明，然后单击 "**下一步**"。  
  
    填写 "密码" 对话框，然后单击 "**下一步**"。  
  
    > [!WARNING]  
    > SQL Server PDW 不支持域管理员或本地管理员密码中的美元符号字符（$）。 包含美元符号的密码将有效并且可用，但可阻止升级和维护活动  
  
    确认新用户说明，然后单击 "**完成**"。  
  
5.  在用户列表中，双击新用户以打开 "用户属性" 对话框。  
  
6.  在 **“隶属于”** 选项卡上，单击 **“添加”**。  
  
    键入**Domain Admins;PdwControlNodeAccess** ，然后单击 "**检查名称**"。 单击“确定”。   
  
    这会将新用户添加到**Domain Admins**组和**PdwControlNodeAccess**组。 单击“确定”。   
  
## <a name="see-also"></a>另请参阅  
[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)  
  
