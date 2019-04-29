---
title: 创建的域管理员的分析平台系统 |Microsoft Docs
description: 某些操作需要分析平台系统域管理员权限。 这解释了如何创建其他设备域管理员。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 852fb3c6cee7c65f8799102bbd65ab368cd0d9e2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63134378"
---
# <a name="create-an-aps-domain-administrator"></a>创建 APS 域管理员
某些操作需要分析平台系统域管理员权限。 这解释了如何创建其他设备域管理员。  
  
## <a name="create-a-domain-administrator"></a>创建域管理员  
拥有足够的权限来配置 AP 的所有节点，运行的用户**APS Configuration Manager** (`dwconfig.exe`) 必须是属于**Domain Admins**组。 若要启动和停止 APS 服务，用户必须是的成员**PdwControlNodeAccess**组。  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>若要将用户添加到 Domain Admins 组  
  
1.  登录到 active AD 节点 **(_装置\_域_-AD01**或**_设备\_域_-AD02**)使用现有的设备域管理员帐户。  
  
2.  在“开始”菜单上，单击“运行”。 在中**开放**框中，键入**dsa.msc**。 单击“确定” 。  
  
3.  在中**Active Directory 用户和计算机**程序中，右键单击**用户**，指向**新建**，然后单击**用户**。  
  
4.  在中**新建对象-用户**对话框中，填写新用户的说明，再单击**下一步**。  
  
    填写密码对话框，再单击**下一步**。  
  
    > [!WARNING]  
    > SQL Server PDW 不支持在域管理员或本地管理员密码的美元符号 （$）。 包含美元符号的密码将有效，可使用，但可以阻止升级和维护活动  
  
    确认新的用户说明，然后依次**完成**。  
  
5.  在用户列表中，双击以打开用户属性对话框中的新用户。  
  
6.  上**隶属**选项卡上，单击**添加**。  
  
    类型**域管理员;PdwControlNodeAccess** ，然后单击**检查名称**。 单击“确定” 。  
  
    这会添加新用户添加到**Domain Admins**组和**PdwControlNodeAccess**组。 单击“确定” 。  
  
## <a name="see-also"></a>请参阅  
[启动配置管理器&#40;分析平台系统&#41;](launch-the-configuration-manager.md)  
  
