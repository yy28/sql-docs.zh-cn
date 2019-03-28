---
title: R 脚本错误和故障排除-SQL Server 机器学习服务
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2df4fa2fd9ef52fe5edbca9440f73f351553f1ed
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511524"
---
# <a name="r-scripting-errors-in-sql-server"></a>SQL Server 中的 R 脚本错误
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 SQL Server 中运行 R 代码时，本文将介绍几个 scriptin gerrors。 列表并不全面。 有很多程序包，并且错误可以同一个包的版本而异。 我们建议在发布脚本错误[Machine Learning Server 论坛](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR)，它支持机器学习 R Services （数据库内）、 Microsoft R Client 和 Microsoft R Server 中使用的组件。

**适用范围：** SQL Server 2016 R Services、 SQL Server 2017 机器学习服务


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>在 T-SQL 或存储过程中将有效的脚本失败

之前将 R 代码包装在存储过程中，它是一个在外部 IDE，或一个如 RTerm 或 RGui 的 R 工具运行 R 代码的好办法。 通过使用这些方法，可以测试和调试的代码通过使用返回详细的错误消息

但是，有时在外部的 IDE 或实用程序中的非常完美的代码可能无法运行存储过程中或在 SQL Server 计算上下文。 如果发生这种情况，有各种问题，查找之前可以假定 SQL Server 中，包不起作用。

1. 检查是否正在运行快速启动板。

2. 查看消息，请参阅的输入的数据或输出数据是否包含具有不兼容或不受支持的数据类型的列。 例如，SQL 数据库查询通常返回 Guid 或 Rowguid，这两者都是不受支持。 有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

3. 查看各个 R 函数，以确定是否所有参数是否都支持 SQL Server 计算上下文的帮助页。 有关 ScaleR 的帮助，使用内联 R 帮助命令，或参阅[包引用](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。

如果 R 运行时正常运行，但您的脚本返回错误，我们建议你尝试调试中专用的 R 开发环境，例如 Visual Studio 的 R 工具的脚本。

我们还建议您查看并稍有重写脚本，更正 R 和数据库引擎之间移动数据时可能出现的数据类型的任何问题。 有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

此外，可以使用 sqlrutils 包捆绑在 R 脚本中作为存储过程更易于使用的格式。 有关详细信息，请参阅：
* [sqlrutils 包](r/ref-r-sqlrutils.md)
* [使用 sqlrutils 创建存储的过程](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>脚本返回不一致的结果

R 脚本可以返回不同的值在 SQL Server 环境中，有几个原因：

- SQL Server 与 R.之间传递数据时，隐式类型转换会自动执行某些数据类型，有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

- 确定位数是一个因素。 例如，通常有 32 位和 64-bit 浮动点库的数学运算的结果中的差异。

- 确定是否在任何操作中生成 Nan。 这可能会使结果无效。

- 执行接近于零的数字倒数时，可以放大的细微差异。

- 累积舍入错误可能会导致小于零时而非零的值等内容。

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>通过 ODBC 远程执行的隐式身份验证

如果连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用的计算机运行 R 命令**RevoScaleR**函数，您可能会遇到错误时使用将数据写入到服务器的 ODBC 调用。 仅当你使用 Windows 身份验证时，会发生此错误。

原因是为 R Services 创建辅助角色帐户没有连接到服务器的权限。 因此，不能代表你执行 ODBC 调用。 因为 SQL 登录名与凭据显式传递从 R 客户端到 SQL Server 实例，再到 ODBC 具有 SQL 登录名不出现问题。 但是，使用 SQL 登录名也是不如使用 Windows 身份验证安全的。

若要启用你的 Windows 凭据从脚本启动了远程的 SQL Server 安全地传递必须模拟你的凭据。 此过程称为_隐式身份验证_。 若要实现此目的，在 SQL Server 计算机运行 R 或 Python 脚本的辅助角色帐户必须具有正确的权限。

1. 打开[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]为你想要运行 R 代码的实例上的管理员。

2. 运行以下脚本。 请务必编辑用户组名称，如果更改了默认值，以及计算机和实例名称。

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>避免在 SQL 计算上下文中运行 R 时清除工作区

尽管在 R 控制台中工作时，清除工作区很常见，但它可以有意外的结果，在 SQL 计算上下文。

`revoScriptConnection` 是包含有关从 SQL Server 调用 R 会话的信息的 R 工作区中的对象。 但是，如果 R 代码包含清除工作区的命令 (如`rm(list=ls())`)，同时清除有关会话以及 R 工作区中的其他对象的所有信息。

解决方法是，SQL Server 中运行 R 时避免随意清除变量和其他对象。 可以通过删除特定的变量**删除**函数：

```R
remove('name1', 'name2', ...)
```

如果有多个要删除的变量，我们建议你将临时变量的名称保存到列表，然后对列表中执行定期垃圾回收。



## <a name="next-steps"></a>后续步骤

[机器学习服务疑难解答和已知的问题](machine-learning-troubleshooting-faq.md)

[数据收集以进行故障排除机器学习](data-collection-ml-troubleshooting-process.md)

[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)

[数据库引擎连接进行故障排除](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
