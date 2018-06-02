---
title: SQL Server 机器学习和 R Services 中的 R 脚本错误 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0b695111849b234f6ca38fc89c538e905f187fb6
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/01/2018
ms.locfileid: "34709096"
---
# <a name="r-scripting-errors-in-sql-server"></a>SQL Server 中的 R 脚本错误
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文记录几个 scriptin gerrors 时在 SQL Server 中运行 R 代码。 列表并不全面。 有许多包，并且错误同一个包的版本间可能不同。 我们建议在上发布脚本错误[机器学习 Server 论坛](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR)，它支持机器学习中 R Services （数据库）、 Microsoft R 客户端和 Microsoft R Server 使用的组件。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>在 T-SQL 中或存储过程中的有效的脚本失败

将 R 代码包装在存储过程中之前, 它是一个外部 IDE，或如 RTerm 或 RGui R 工具之一中运行 R 代码的好办法。 通过使用这些方法，你可以测试和调试的代码通过使用由。 详细的错误消息

但是，有时可正常运行在外部 IDE 或实用程序中的代码可能无法运行存储过程中或在 SQL Server 计算上下文。 如果发生这种情况，有各种问题，若要寻找之前可以假定包无法在 SQL Server 中工作。

1. 检查是否正在运行快速启动板。

2. 查看消息的输入的数据或输出数据是否包含具有不兼容或不受支持的数据类型的列。 例如，在 SQL 数据库上的查询通常返回 Guid 或 Rowguid，二者都是不受支持。 有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

3. 查看各个 R 函数，以确定所有参数是否都支持 SQL Server 计算上下文的帮助页。 ScaleR 的帮助，请使用内联 R 帮助命令，或请参阅[程序包引用](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。

如果 R 运行时正常工作，但你的脚本返回错误，我们建议你尝试在专用的 R 开发环境，如 R Tools for Visual Studio 中的脚本调试。

我们还建议你查看并略有重写脚本，以更正任何问题与 R 和数据库引擎之间移动数据时，可能会出现的数据类型。 有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

此外，你可以使用 sqlrutils 包将 R 脚本捆绑中的存储过程的过程更轻松地使用的格式。 有关详细信息，请参阅：
* [通过使用 sqlrutils 包生成的 R 代码的存储的过程](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
* [通过使用 sqlrutils 创建存储的过程](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>脚本返回不一致的结果

R 脚本可以在 SQL Server 环境中，返回不同的值，原因有多种：

- 当 SQL Server 和。 之间传递数据自动上某些数据类型，执行隐式类型转换有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

- 确定位数是一个因素。 例如，通常有 32 位和 64 位浮点点库的数学运算的结果中的差异。

- 确定是否在任何操作生成 Nan。 这可能会使结果无效。

- 当你拍摄接近于零的数字的倒数时，可以放大细微差异。

- 累积的舍入误差可能会导致小于零时而不是零的值之类的内容。

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>通过 ODBC 远程执行的的默示身份验证

如果你连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]计算机，以便运行 R 命令通过使用**RevoScaleR**函数时可能会出现错误使用将数据写入到服务器的 ODBC 调用。 仅在你使用 Windows 身份验证时，将发生此错误。

原因是为 R Services 创建的工作帐户没有权限来连接到服务器。 因此，不能代表你执行 ODBC 调用。 因为具有 SQL 登录名的凭据通过显式从 R 客户端到 SQL Server 实例，然后执行到 ODBC 具有 SQL 登录名未出现该问题。 但是，使用 SQL 登录名也是比使用 Windows 身份验证的安全级别较低的。

若要启用您的 Windows 凭据启动了远程的 SQL Server 脚本从安全地传递必须模拟你的凭据。 此过程称为_默示身份验证_。 若要完成此操作，请在 SQL Server 计算机运行 R 或 Python 脚本辅助帐户必须具有正确的权限。

1. 打开[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]为你想要运行 R 代码的实例上的管理员。

2. 运行以下脚本。 请务必编辑该用户组名称，如果更改了默认值和的计算机和实例名称。

    ```SQL
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>避免当在 SQL 计算上下文中运行 R 时清除工作区

尽管在 R 控制台工作时，清除工作区中均相同，但它可以有 SQL 中的意外的后果计算上下文。

`revoScriptConnection` 是包含有关从 SQL Server 调用 R 会话的信息的 R 工作区中的对象。 但是，如果 R 代码中包含的命令以清除工作区 (如`rm(list=ls())`)，以及清除有关会话和 R 工作区中的其他对象的所有信息。

一种解决方法，避免不加选择地清除的变量和其他对象，当 SQL Server 中运行 R 时。 你可以通过使用删除特定变量**删除**函数：

```R
remove('name1', 'name2', ...)
```

如果有多个要删除的变量，我们建议你将临时变量的名称保存到列表，然后执行列表上的定期垃圾回收。



## <a name="next-steps"></a>后续步骤

[机器学习服务疑难解答和已知的问题](machine-learning-troubleshooting-faq.md)

[进行故障排除机器学习的数据收集](data-collection-ml-troubleshooting-process.md)

[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)

[数据库引擎连接进行故障排除](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
