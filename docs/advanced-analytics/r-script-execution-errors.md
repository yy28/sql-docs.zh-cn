---
title: R 脚本错误和疑难解答
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 83029a9727a26c647d78c49501fde08f72d7694d
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343402"
---
# <a name="r-scripting-errors-in-sql-server"></a>SQL Server 中的 R 脚本错误
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍了在 SQL Server 中运行 R 代码时的多个 .scriptin gerrors。 该列表并不全面。 存在许多包, 并且错误在同一包的不同版本之间可能会有所不同。 建议在[Machine Learning Server 论坛](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR)上发布脚本错误, 该论坛支持 R Services (数据库中)、Microsoft R Client 和 Microsoft R Server 中使用的机器学习组件。

**适用范围：** SQL Server 2016 R Services SQL Server 2017 机器学习服务


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>T-sql 或存储过程中的有效脚本失败

在将 R 代码包装在存储过程中之前, 最好是在外部 IDE 或某个 R 工具 (如 Rterm.exe 或 Rgui.exe) 中运行 R 代码。 通过使用这些方法, 您可以使用 R 返回的详细错误消息来测试和调试代码。

但是, 有时在外部 IDE 或实用程序中正常工作的代码可能无法在存储过程或 SQL Server 计算上下文中运行。 如果发生这种情况, 则在您假设包在 SQL Server 中无法正常工作之前, 需要查找各种问题。

1. 检查启动板是否正在运行。

2. 查看消息以查看输入数据或输出数据是否包含数据类型不兼容或不受支持的列。 例如, SQL 数据库上的查询通常返回 Guid 或 Rowguid, 这两者都不受支持。 有关详细信息, 请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

3. 查看各个 R 函数的帮助页, 以确定 SQL Server 计算上下文是否支持所有参数。 有关 ScaleR 帮助, 请使用 inline R 帮助命令, 或参阅[包引用](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。

如果 R 运行时运行正常, 但您的脚本返回错误, 我们建议您尝试在专用的 R 开发环境 (例如针对 Visual Studio 的 R 工具) 中调试脚本。

我们还建议你查看并略微重写脚本, 以更正在 R 和数据库引擎之间移动数据时可能出现的数据类型的任何问题。 有关详细信息, 请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

此外, 还可以使用 sqlrutils 包以更易于作为存储过程使用的格式来捆绑 R 脚本。 有关详细信息，请参阅：
* [sqlrutils 包](r/ref-r-sqlrutils.md)
* [使用 sqlrutils 创建存储过程](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>脚本返回不一致的结果

出于以下几个原因, R 脚本可以在 SQL Server 上下文中返回不同的值:

- 当数据在 SQL Server 和 R 之间传递时, 会自动对某些数据类型执行隐式类型转换。有关详细信息, 请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

- 确定位数是否为因素。 例如, 对于32位和64位浮点库, 数学运算的结果经常有所不同。

- 确定是否在任何操作中生成了 Nan。 这可能会使结果无效。

- 如果使用接近零的值, 则可能会使小差异放大。

- 累积舍入错误可能导致值小于零的值, 而不是零。

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>通过 ODBC 进行远程执行的隐式身份验证

如果使用**RevoScaleR**函数连接[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到计算机以运行 R 命令, 则在使用向服务器写入数据的 ODBC 调用时可能会收到错误。 仅当你使用 Windows 身份验证时, 才会发生此错误。

原因是为 R Services 创建的工作线程帐户没有连接到服务器的权限。 因此, 无法代表您执行 ODBC 调用。 SQL 登录名不会出现此问题, 因为在 SQL 登录名中, 凭据将从 R 客户端显式传递到 SQL Server 实例, 然后传递到 ODBC。 但是, 使用 SQL 登录名也不如使用 Windows 身份验证安全。

若要使您的 Windows 凭据能够安全地从远程启动的脚本进行传递, SQL Server 必须模拟您的凭据。 此过程称为_隐含身份验证_。 要执行此操作, 在 SQL Server 计算机上运行 R 或 Python 脚本的辅助角色帐户必须具有正确的权限。

1. 在[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]要运行 R 代码的实例上以管理员身份打开。

2. 运行以下脚本。 如果更改了默认值、计算机名称和实例名称, 请务必编辑用户组名称。

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>在 SQL 计算上下文中运行 R 时避免清除工作区

尽管在 R 控制台中工作时清除工作区很常见, 但它可能会在 SQL 计算上下文中产生意想不到的后果。

`revoScriptConnection`是 R 工作区中的对象, 其中包含有关从 SQL Server 调用的 R 会话的信息。 但是, 如果你的 R 代码包含用于清除工作区的命令 (如`rm(list=ls())`), 则还会清除有关此会话和 R 工作区中其他对象的所有信息。

一种解决方法是, 在 SQL Server 中运行 R 时避免任意清除变量和其他对象。 可以通过使用**remove**函数删除特定的变量:

```R
remove('name1', 'name2', ...)
```

如果有多个要删除的变量, 则建议您将临时变量的名称保存到列表中, 然后对该列表执行定期垃圾回收。



## <a name="next-steps"></a>后续步骤

[机器学习服务疑难解答和已知问题](machine-learning-troubleshooting-faq.md)

[计算机学习疑难解答的数据收集](data-collection-ml-troubleshooting-process.md)

[升级和安装常见问题解答](r/upgrade-and-installation-faq-sql-server-r-services.md)

[数据库引擎连接疑难解答](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
