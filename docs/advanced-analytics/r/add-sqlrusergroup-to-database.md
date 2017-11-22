---
title: "作为数据库用户添加 SQLRUserGroup |Microsoft 文档"
ms.custom: 
ms.date: 11/13/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "默示身份验证"
- SQLRUserGroup
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 97a571a9a91ac31e955f6833e27a975f87267218
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>作为数据库用户添加 SQLRUserGroup

在安装的过程[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]或[!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]，用于运行下的安全令牌的任务创建的新 Windows 用户帐户[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服务。 当用户发送的机器学习脚本从外部客户端，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]激活可用的工作帐户、 将其映射到的调用用户的标识并运行代表用户脚本。 这一新的数据库引擎服务支持调用的外部脚本的安全执行*默示身份验证*。

你可以在 Windows 用户组中查看这些帐户**SQLRUserGroup**。 默认情况下，被创建 20 工作人员帐户，这通常是绰绰有余用于运行 R 作业。

但是，如果你需要从远程数据科学客户端运行 R 脚本，且正在使用 Windows 身份验证，你必须授予这些辅助帐户权限登录到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代表你的实例。

## <a name="add-sqlrusergroup-as-a-sql-server-login"></a>将 SQLRUserGroup 添加为 SQL Server 登录名

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“对象资源管理器”中，展开“安全性” ，右键单击“登录名” ，然后选择“新建登录名” 。

2. 在**登录名-新建**对话框中，选择**搜索**。 （不要输入任何内容在框中尚未。）
    
     ![单击搜索以添加机器学习的新登录名](media/implied-auth-login1.png "单击搜索以添加机器学习的新登录名")

3. 在**选择用户或组**框中，单击**对象类型**按钮。

     ![搜索要添加机器学习的新登录名的对象类型](media/implied-auth-login2.png "搜索要添加机器学习的新登录名的对象类型")

4. 在**对象类型**对话框中，选择**组**。 清除所有其他复选框。

     ![在对象类型对话框中选择组](media/implied-auth-login3.png "对象类型对话框中选择的组")

4. 单击**高级**，验证，要搜索的位置为当前计算机，然后单击**立即查找**。

     ![单击开始查找来获取组列表](media/implied-auth-login4.png "单击立即查找若要获取的组的列表")

5. 直到找到一个开头的服务器上的组帐户的列表中滚动`SQLRUserGroup`。
    
    + 与的快速启动板服务关联组的名称_默认实例_只始终是**SQLRUserGroup**。 选择此帐户仅对于默认实例。
    + 如果你使用_命名实例_，实例名称追加到的默认名称`SQLRUserGroup`。 因此，如果你的实例名为"MLTEST"，此实例的默认用户组名称将**SQLRUserGroupMLTest**。
 
     ![服务器上的组的示例](media/implied-auth-login5.png "服务器上的组的示例")
   
5. 单击**确定**以关闭高级的搜索对话框。

    > [!IMPORTANT]
    > 请确保你已选择正确的帐户的实例。 每个实例可以使用其自己的快速启动板服务和为该服务创建的组。 实例不能共享快速启动板服务或辅助帐户。

6. 单击**确定**一次以关闭**选择用户或组**对话框。

7. 在**登录名-新建**对话框中，单击**确定**。 默认情况下，将登录名分配到 **公共** 角色，且有权连接到数据库引擎。

## <a name="change-the-number-of-worker-accounts-in-sqlrusergroup"></a>更改辅助帐户中 SQLRUserGroup 数

如果你想要的机器学习的大量使用，则可以增加用于运行外部脚本，如本文中所述的帐户数： 

+ [修改用户帐户池的机器学习](modify-the-user-account-pool-for-sql-server-r-services.md)

默认情况下，20 创建帐户，它支持 20 的并发会话。 并行化的任务也不会占用额外的帐户。 例如，如果用户运行使用并行处理的评分任务时，相同的工作线程帐户将重复的所有线程使用。