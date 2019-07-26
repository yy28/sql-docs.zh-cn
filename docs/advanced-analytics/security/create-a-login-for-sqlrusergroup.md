---
title: 为 SQLRUserGroup 创建登录名
description: 对于使用隐含身份验证的环回连接, 请在 SQL Server 中为 SQLRUserGroup 创建一个登录名, 以便辅助角色帐户可以登录到服务器, 以便将身份转换回调用用户。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f86bedc3cfd92272b500d5d3edd701b6ca51d38b
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469991"
---
# <a name="create-a-login-for-sqlrusergroup"></a>为 SQLRUserGroup 创建登录名
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

如果脚本中的[环回连接](../../advanced-analytics/concepts/security.md#implied-authentication)指定了*可信连接*, 并且用于执行对象的标识是 Windows 用户帐户, 则在 SQL Server for [SQLRUserGroup](../concepts/security.md#sqlrusergroup)中创建一个[登录名](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login)。

可信连接是`Trusted_Connection=True`在连接字符串中的连接。 当 SQL Server 收到指定可信连接的请求时, 它会检查当前 Windows 用户的标识是否具有登录名。 对于作为工作线程帐户执行的外部进程 (例如**SQLRUserGroup**中的 MSSQLSERVER01), 请求会失败, 因为默认情况下, 这些帐户不具有登录名。

可以通过创建**SQLServerRUserGroup**的登录名来解决连接错误。 有关标识和外部进程的详细信息, 请参阅[扩展性框架的安全性概述](../concepts/security.md)。

> [!Note]
> 请确保**SQLRUserGroup**具有 "允许在本地登录" 权限。 默认情况下, 此权限授予所有新的本地用户, 但某些组织更严格的组策略可能会禁用此权限。

## <a name="create-a-login"></a>创建登录名

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“对象资源管理器”中，展开“安全性” ，右键单击“登录名” ，然后选择“新建登录名” 。

2. 在 "**登录名-新建**" 对话框中, 选择 "**搜索**"。 (请不要在该框中键入任何内容。)
    
     ![单击 "搜索" 为机器学习添加新的登录名](media/implied-auth-login1.png "单击 \"搜索\" 为机器学习添加新的登录名")

3. 在 "**选择用户或组**" 框中, 单击 "**对象类型**" 按钮。

     ![搜索对象类型以添加机器学习的新登录名](media/implied-auth-login2.png "搜索对象类型以添加机器学习的新登录名")

4. 在 "**对象类型**" 对话框中, 选择 "**组**"。 清除所有其他复选框。

     "![选择对象类型中的组" 对话框]"(media/implied-auth-login3.png "选择对象类型中的组\" 对话框")

4. 单击 "**高级**", 验证要搜索的位置是否为当前计算机, 然后单击 "**立即查找**"。

     ![单击 "立即查找" 获取组列表](media/implied-auth-login4.png "单击 \"立即查找\" 获取组列表")

5. 在服务器上的组帐户列表中滚动, 直到找到一个开始处`SQLRUserGroup`。
    
    + 与_默认实例_的启动板服务关联的组名称始终是**SQLRUserGroup**, 无论你是安装 R 还是 Python, 都是如此。 只为默认实例选择此帐户。
    + 如果使用的是_命名实例_, 则会将实例名称附加到默认辅助角色组名称的名称中`SQLRUserGroup`。 例如, 如果实例名为 "MLTEST", 则此实例的默认用户组名称将为**SQLRUserGroupMLTest**。
 
    ![服务器上的组示例](media/implied-auth-login5.png "服务器上的组示例")
   
5. 单击 **"确定"** 以关闭 "高级搜索" 对话框。

    > [!IMPORTANT]
    > 请确保已为实例选择了正确的帐户。 每个实例只能使用其自己的启动板服务和为该服务创建的组。 实例不能共享快速启动板服务或辅助角色帐户。

6. 再单击 **"确定"** 以关闭 "**选择用户或组**" 对话框。

7. 在 "**登录名-新建**" 对话框中, 单击 **"确定"** 。 默认情况下，将登录名分配到 **公共** 角色，且有权连接到数据库引擎。

## <a name="next-steps"></a>后续步骤

+ [安全性概述](../concepts/security.md)
+ [扩展性框架](../concepts/extensibility-framework.md)
