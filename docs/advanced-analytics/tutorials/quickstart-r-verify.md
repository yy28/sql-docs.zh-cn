---
title: 用于验证 R 是否存在于 SQL Server 中的快速入门
description: 快速入门, 验证 SQL Server 中是否存在 R 和机器学习服务。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 072a6f34a7cb91505d77356d6ec3835915c310d0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715400"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>快速入门：验证 SQL Server 中是否存在 R 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 包括对常驻 SQL Server 数据进行数据科学分析的 R 语言支持。 你的 R 脚本可以包含开放源代码 R 函数、第三方库或内置的 Microsoft R 库, 如用于大规模预测分析的[RevoScaleR](../r/revoscaler-overview.md) 。

使用以下两种方法之一通过存储过程执行脚本:

+ 内置的[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)存储过程, 将 R 脚本作为输入参数传入。
+ 在您创建的[自定义存储过程](sqldev-in-database-r-for-sql-developers.md)中包装 R 脚本。

在本快速入门中, 你将验证是否安装并配置了[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)或[SQL Server 2016 R Services](../r/sql-server-r-services.md) 。

## <a name="prerequisites"></a>系统必备

此练习需要使用已安装以下项之一的 SQL Server 实例的访问权限:

+ [SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md), 已安装 R 语言
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

SQL Server 实例可位于 Azure 虚拟机或本地。 请注意, 默认情况下禁用外部脚本功能, 因此在开始之前, 您可能需要[启用外部脚本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并验证**SQL Server Launchpad 服务**是否正在运行。

还需要一个用于运行 SQL 查询的工具。 您可以使用任何数据库管理或查询工具来运行 R 脚本, 前提是它可以连接到 SQL Server 实例, 并运行 T-sql 查询或存储过程。 本快速入门使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="verify-r-exists"></a>验证 R 是否存在

你可以确认为你的 SQL Server 实例启用了机器学习服务 (with R) 以及安装了哪个版本的 R。 请按照以下步骤操作。

1. 打开 SQL Server Management Studio, 然后连接到 SQL Server 实例。

2. 运行以下代码。 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. R `print`函数将该版本返回到 "**消息**" 窗口。 在下面的示例输出中, 可以看到, 在此示例中 SQL Server 安装了 R 版本3.3.3。

    **结果**

    ```text
    platform       x86_64-w64-mingw32          
    arch           x86_64                      
    os             mingw32                     
    system         x86_64, mingw32             
    status                                     
    major          3                           
    minor          3.3                         
    year           2017                        
    month          03                          
    day            06                          
    svn rev        72310                       
    language       R                           
    version.string R version 3.3.3 (2017-03-06)
    nickname       Another Canoe               
    ```

如果从此查询收到任何错误, 请排除任何安装问题。 若要启用外部代码库, 必须安装安装后配置。 请参阅[install SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)或[安装 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)。 同样, 请确保启动板服务正在运行。

取决于你的环境，你可能需要使 R 辅助角色帐户能够连接到 SQL Server，安装额外的网络库，启用远程代码执行，或者在配置所有项后重新启动实例。 有关详细信息, 请参阅[R Services 安装和升级常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

## <a name="list-r-packages"></a>列出 R 包

Microsoft 在 SQL Server 实例中提供了许多与机器学习服务预装的 R 包。 若要查看安装了哪些 R 包的列表, 包括版本、依赖项、许可证和库路径信息, 请执行以下步骤。

1. 在 SQL Server 实例上运行以下脚本。

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. 输出来自`installed.packages()` R 并作为结果集返回。

    **结果**

    ![R 中安装的包](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>后续步骤

现在, 你已确认你的实例已准备好使用 R, 接下来请仔细查看一下基本的 R 交互。

> [!div class="nextstepaction"]
> [起步SQL Server 中的 "Hello world" R 脚本](quickstart-r-run-using-tsql.md)
