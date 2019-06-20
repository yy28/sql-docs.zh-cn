---
title: 为 SQLRUserGroup 的 SQL Server 机器学习服务创建一个登录名
description: 对于使用隐式身份验证的环回连接，创建登录名在 SQL Server 中为 SQLRUserGroup，以便辅助角色帐户可以登录到服务器，用于返回到调用用户标识转换。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 62dd1ddf61c3cc2e1340619566ad9f4dcce062b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642088"
---
# <a name="create-a-login-for-sqlrusergroup"></a>为 SQLRUserGroup 创建登录名
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

创建[SQL Server 中的登录名](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login)有关[SQLRUserGroup](../concepts/security.md#sqlrusergroup)时[循环连接](../../advanced-analytics/concepts/security.md#implied-authentication)在脚本中指定*可信连接*，和用于执行对象的标识包含你的代码是 Windows 用户帐户。

受信任的连接是必须`Trusted_Connection=True`连接字符串中。 当 SQL Server 收到指定的受信任的连接请求时，它会检查当前的 Windows 用户的标识是否具有登录名。 对于作为辅助角色帐户正在执行的外部进程 (如从 MSSQLSERVER01 **SQLRUserGroup**)，请求失败，因为这些帐户默认情况下将不具有登录名。

可以通过创建一个登录名来解决连接错误**SQLServerRUserGroup**。 有关标识和外部进程的详细信息，请参阅[的可扩展性框架安全概述](../concepts/security.md)。

> [!Note]
> 请确保**SQLRUserGroup**具有"允许本地登录"权限。 默认情况下，此权限已授予给所有新的本地用户，但一些组织更严格的组策略可能会禁用此权限。

## <a name="create-a-login"></a>创建登录名

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
    + 如果使用的_命名实例_，实例名追加到默认的辅助角色组名称，名称`SQLRUserGroup`。 例如，如果你的实例名为"MLTEST"，此实例的默认用户组名称将是**SQLRUserGroupMLTest**。
 
    ![服务器上的组的示例](media/implied-auth-login5.png "服务器上的组的示例")
   
5. 单击**确定**以关闭高级的搜索对话框。

    > [!IMPORTANT]
    > 请确保已选择正确的实例的帐户。 每个实例可以使用其自己的快速启动板服务和该服务创建的组。 实例不能共享快速启动板服务或辅助角色帐户。

6. 单击**确定**一次以关闭**选择用户或组**对话框。

7. 在中**登录名-新建**对话框中，单击**确定**。 默认情况下，将登录名分配到 **公共** 角色，且有权连接到数据库引擎。

## <a name="next-steps"></a>后续步骤

+ [安全性概述](../concepts/security.md)
+ [可扩展性框架](../concepts/extensibility-framework.md)
