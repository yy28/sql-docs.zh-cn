---
title: SQL Server 中存在验证 R 快速入门
description: 用于验证 R 和机器学习服务中存在的 SQL Server 的快速入门。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2bd9e43232b77bc77611b0c4cd5285b69c9a6261
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046769"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>快速入门：验证 SQL Server 中存在 R 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 包括对数据科学驻留的 SQL Server 数据分析的 R 语言支持。 在 R 脚本可以包含的开放源代码 R 函数、 第三方 R 库或内置的 Microsoft R 库等[RevoScaleR](../r/revoscaler-overview.md)用于在规模较大的预测分析。

脚本执行是通过存储过程，使用以下方法之一：

+ 内置[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)存储过程，传递作为输入参数中的 R 脚本。
+ 包装中的 R 脚本[自定义存储过程](sqldev-in-database-r-for-sql-developers.md)你创建的。

在此快速入门中，您将验证[SQL Server 2017 机器学习服务](../what-is-sql-server-machine-learning.md)或[SQL Server 2016 R Services](../r/sql-server-r-services.md)安装和配置。

## <a name="prerequisites"></a>先决条件

本演练需要访问 SQL Server 的实例与已安装以下项之一：

+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)，与安装的 R 语言
+ [SQL Server 2016 R 服务](../install/sql-r-services-windows-install.md)

SQL Server 实例可以是 Azure 虚拟机或本地。 只需注意，外部脚本编写功能默认处于禁用状态，因此可能需要[启用外部脚本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并确认**SQL Server Launchpad 服务**在开始之前运行。

您还需要用于运行 SQL 查询的工具。 可以运行使用任何数据库管理的 R 脚本或查询工具，前提是它可以连接到 SQL Server 实例，并运行 T-SQL 查询或存储的过程。 本快速入门使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="verify-r-exists"></a>验证存在 R

你可以确认为您的 SQL Server 实例和安装的 R 版本启用了机器学习服务 （使用 R)。 按照以下步骤。

1. 打开 SQL Server Management Studio 并连接到 SQL Server 实例。

2. 运行下面的代码。 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. R`print`函数将返回到新版本**消息**窗口。 在下面的示例输出中，您可以看到 SQL Server 在这种情况下具有 R 版本 3.3.3 安装。

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

如果此查询中获取的任何错误，请排除任何安装问题。 安装后则需要配置才能启用对外部代码库的使用。 请参阅[安装 SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)或[安装 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)。 同样，请确保快速启动板服务正在运行。

取决于你的环境，你可能需要使 R 辅助角色帐户能够连接到 SQL Server，安装额外的网络库，启用远程代码执行，或者在配置所有项后重新启动实例。 有关详细信息，请参阅[R Services 的安装和升级常见问题](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

## <a name="list-r-packages"></a>列出 R 包

Microsoft 提供大量预装了机器学习服务中的 SQL Server 实例的 R 包。 若要查看列表中的哪些 R 包安装，包括版本、 依赖项、 许可证和库路径信息，请按照以下步骤。

1. SQL Server 实例上运行以下脚本。

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. 输出是从`installed.packages()`在 R 中，并返回结果集。

    **结果**

    ![在 R 中安装包](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>后续步骤

现在，已确认你的实例已准备好使用 R，则需要进一步了解基本的 R 交互。

> [!div class="nextstepaction"]
> [快速入门：SQL Server 中的"hello world"R 脚本 ](quickstart-r-run-using-tsql.md)
