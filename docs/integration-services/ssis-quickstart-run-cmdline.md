---
title: "在命令提示符下运行 SSIS 包 |Microsoft 文档"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: a33b8518ec3284f5de73d38c87209057dc1c7487
ms.contentlocale: zh-cn
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>与 DTExec.exe 的命令提示符下运行 SSIS 包
本快速入门教程演示如何从命令提示符下运行 SSIS 包，通过运行`DTExec.exe`结合适当的参数。

> [!NOTE]
> 本文中所述的方法未经过测试与包部署到 Azure SQL 数据库服务器。

有关详细信息`DTExec.exe`，请参阅[dtexec 实用工具](https://docs.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility)。

## <a name="run-a-package-with-dtexec"></a>使用 dtexec 运行包

如果该文件夹，包含`DTExec.exe`不在你`path`环境变量，你可能需要使用`cd`命令转到其目录。 对于 SQL Server 自 2017 年，此文件夹通常是`C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`。

使用下面的示例中使用的参数值，程序运行包在 SSIS 服务器上-即，托管 SSIS 目录数据库 (SSISDB) 的服务器中指定的文件夹路径中。 `/Server`参数提供服务器的名称。 程序将作为当前用户使用 Windows 集成身份验证连接。 若要使用 SQL 身份验证，指定`/User`和`Password`替换相应的值的参数。

1. 打开命令提示符窗口。

2. 运行`DTExec.exe`并为至少提供值`ISServer`和`Server`参数，如下面的示例中所示：

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>后续步骤
- 考虑运行包的其他方式。
    - [使用 SSMS 中运行 SSIS 包](./ssis-quickstart-run-ssms.md)
    - [运行 SSIS 包使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 运行 SSIS 包](ssis-quickstart-run-tsql-vscode.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 

