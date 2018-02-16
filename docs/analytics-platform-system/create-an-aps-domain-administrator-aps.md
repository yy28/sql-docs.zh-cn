---
title: "创建一个 AP 域管理员 (AP)"
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
ms.assetid: ed52bf78-2b0a-4252-98a7-8c2805e22d3d
caps.latest.revision: 
ms.openlocfilehash: 0ebc616d28fe734b9dac52303641390ce9bc0957
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="create-an-aps-domain-administrator"></a>创建一个 AP 域管理员
某些操作需要 Analytics Platform System 域管理员权限。 本部分说明如何创建其他设备域管理员。  
  
## <a name="create-a-domain-administrator"></a>创建域管理员  
具有足够的权限来配置运行的用户的所有 AP 节点， **AP Configuration Manager** (`dwconfig.exe`) 必须是属于**Domain Admins**组。 若要启动和停止 AP 服务，用户必须是属于**PdwControlNodeAccess**组。  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>若要将用户添加到 Domain Admins 组  
  
1.  登录到活动的 AD 节点**(*appliance_domain*-AD01**或 ***appliance_domain *-AD02**) 使用现有的设备域管理员帐户。  
  
2.  在“开始”菜单上，单击“运行”。 在**打开**框中，键入**dsa.msc**。 单击 **“确定”**。  
  
3.  在**Active Directory 用户和计算机**程序中，右键单击**用户**，指向**新建**，然后单击**用户**。  
  
4.  在**新建对象 – 用户**对话框中，填写的新用户的说明，然后单击**下一步**。  
  
    填写密码对话框中，然后单击**下一步**。  
  
    > [!WARNING]  
    > SQL Server PDW 不支持美元符号 （$） 中的域管理员或本地管理员密码。 包含美元符号的密码将有效，可以使用，但可以阻止升级和维护活动  
  
    确认新的用户说明，，然后单击**完成**。  
  
5.  在用户列表中，双击新用户，以打开用户属性对话框中。  
  
6.  上**隶属于**选项卡上，单击**添加**。  
  
    类型**Domain Admins;PdwControlNodeAccess** ，然后单击**检查名称**。 单击 **“确定”**。  
  
    这将添加新用户添加到**Domain Admins**组和**PdwControlNodeAccess**组。 单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md)  
  
