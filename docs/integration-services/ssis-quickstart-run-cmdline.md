---
title: "从命令提示符运行 SSIS 包 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c2b83605714e01961c50d71e83ba57691bc3833
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>使用 DTExec.exe 从命令提示符运行 SSIS 包
本快速入门教程演示如何通过运行包含相应参数的 `DTExec.exe`，从命令提示符处运行 SSIS 包。

> [!NOTE]
> 本文介绍的方法尚未使用部署到 Azure SQL 数据库服务器的包进行测试。

有关 `DTExec.exe` 的详细信息，请参阅 [dtexec 实用工具](https://docs.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility)。

## <a name="run-a-package-with-dtexec"></a>使用 dtexec 运行包

如果包含 `DTExec.exe` 的文件夹不在 `path` 环境变量中，可能需要使用 `cd` 命令将目录更改为该文件夹的目录。 对于 SQL Server 2017，此文件夹通常位于 `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`。

使用下面的示例中所用的参数值，程序会运行 SSIS 服务器（即承载 SSIS 目录数据库 (SSISDB) 的服务器）上指定的文件夹路径中的包。 `/Server` 参数提供服务器名称。 程序以当前用户的身份使用 Windows 集成身份验证进行连接。 若要使用 SQL 身份验证，请使用合适的值指定 `/User` 和 `Password` 参数。

1. 打开命令提示符窗口。

2. 如下面的示例中所示，运行 `DTExec.exe` 并至少提供 `ISServer` 和 `Server` 参数的值：

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>后续步骤
- 考虑运行包的其他方式。
    - [使用 SSMS 运行 SSIS 包](./ssis-quickstart-run-ssms.md)
    - [使用 Transact-SQL (SSMS) 运行 SSIS 包](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 Transact-SQL (VS Code) 运行 SSIS 包](ssis-quickstart-run-tsql-vscode.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)
    - [使用 C# 运行 SSIS 包](./ssis-quickstart-run-dotnet.md) 
