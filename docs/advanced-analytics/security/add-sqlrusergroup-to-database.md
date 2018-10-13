---
title: 将 SQLRUserGroup 添加为数据库用户 （SQL Server 机器学习） |Microsoft Docs
description: 如何为 SQL Server 机器学习服务将 SQLRUserGroup 添加为数据库用户。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fc5294453def64d13cc43a74a8a5fb299c3e23e3
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100318"
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>将 SQLRUserGroup 添加为数据库用户
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

创建数据库登录名[SQLRUserGroup](../concepts/security.md#sqlrusergroup)以允许来自 R 和 Python 脚本，如果目标是数据或 SQL Server 实例上的操作的受信任的连接。 

对于包含连接字符串用于 SQL Server 登录名或完全指定的用户名和密码的脚本，创建登录名不是必需。

## <a name="when-a-login-is-required"></a>需要一个登录名时

如果 R 或 Python 脚本包含一个连接字符串，指定受信任的连接 (例如，"Trusted_Connection = True")，其他配置是对 SQL Server 所需的正确表示法的用户标识。 外部进程下运行**SQLRUserGroup**辅助角色帐户，如 MSSQLSERVER01，受信任的用户显示辅助标识。 由于此标识具有 SQL Server 没有登录名的权限，受信任的连接将失败，除非您将添加**SQLRUserGroup**作为数据库用户。 有关详细信息，请参阅[*隐式身份验证*](../../advanced-analytics/concepts/security.md#implied-authentication)。

前面曾提到快速启动板保留原始调用该脚本，并运行进程的辅助角色帐户的用户的映射。 受信任的连接成功后的辅助角色帐户，原始调用用户的标识将接管，用于检索数据。 不需要将 db_datareader 权限授予**SQLRUserGroup**。

> [!Note]
>  请确保**SQLRUserGroup**具有"允许本地登录"权限。 默认情况下，此权限已授予给所有新的本地用户，但在某些组织可能会强制实施更严格的组策略。

## <a name="create-a-login"></a>创建登录

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“对象资源管理器”中，展开“安全性” ，右键单击“登录名” ，然后选择“新建登录名” 。

2. 在中**登录名-新建**对话框中，选择**搜索**。 （无任何内容在框中键入尚未。）
    
     ![单击搜索以添加新的登录名为机器学习](media/implied-auth-login1.png "单击搜索以添加新的登录名为机器学习")

3. 在中**选择用户或组**框中，单击**对象类型**按钮。

     ![搜索要添加的机器学习的新登录名的对象类型](media/implied-auth-login2.png "搜索要添加的机器学习的新登录名的对象类型")

4. 在中**对象类型**对话框中，选择**组**。 清除所有其他复选框。

     ![在对象类型对话框中选择组](media/implied-auth-login3.png "对象类型对话框中选择组")

4. 单击**高级**，验证要搜索的位置是当前计算机，然后单击**立即查找**。

     ![单击开始查找来获取组的列表](media/implied-auth-login4.png "单击立即查找以获取组的列表")

5. 滚动浏览列表，直到找到一个开始在服务器上的组帐户的`SQLRUserGroup`。
    
    + 与的 Launchpad 服务关联的组的名称_默认实例_始终**SQLRUserGroup**，无论是否安装了 R 或 Python。 选择此帐户的默认实例。
    + 如果使用的_命名实例_，实例名追加到默认的辅助角色组名称，名称`SQLRUserGroup`。 因此，如果你的实例名为"MLTEST"，此实例的默认用户组名称将是**SQLRUserGroupMLTest**。
 
     ![服务器上的组的示例](media/implied-auth-login5.png "服务器上的组的示例")
   
5. 单击**确定**以关闭高级的搜索对话框。

    > [!IMPORTANT]
    > 请确保已选择正确的实例的帐户。 每个实例可以使用其自己的快速启动板服务和该服务创建的组。 实例不能共享快速启动板服务或辅助角色帐户。

6. 单击**确定**一次以关闭**选择用户或组**对话框。

7. 在中**登录名-新建**对话框中，单击**确定**。 默认情况下，将登录名分配到 **公共** 角色，且有权连接到数据库引擎。