---
title: 升级包含数据库单元测试的较旧的测试项目 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 42782ff3-e8cf-4c9d-8dac-a95b236edfc4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b2ad973cf845817a0dbd251bbee23ac6f13d7c04
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110579"
---
# <a name="upgrade-an-older-test-project-containing-database-unit-tests"></a>升级包含数据库单元测试的较旧的测试项目
可以升级在 Visual Studio 2010 中创建的、包含数据库单元测试的较旧测试项目，以使用新的 SQL Server Data Tools 数据库单元测试运行时和工具。 升级较旧项目后，可以向该项目添加 SQL Server 单元测试（有关详细信息，请参见[创建和定义 SQL Server 单元测试](../ssdt/creating-and-defining-sql-server-unit-tests.md)）。  
  
> [!TIP]  
> 如果你正在使用 Visual Studio 2010，则在将 SQL Server 单元测试添加到测试项目后，不应使用较旧数据库单元测试模板添加单元测试。 如果这样做，将需要再次转换项目，之后测试才能正确执行。  
  
如果具有在早于 Visual Studio 2010 的版本中创建的测试数据库项目，则可以使用[如何：从以前版本的 Visual Studio 升级数据库单元测试](https://msdn.microsoft.com/library/dd193412(VS.100).aspx)中的信息将数据库项目升级到 Visual Studio 2010，然后再将项目升级到 SQL Server Data Tools。  
  
### <a name="initiating-an-upgrade"></a>启动升级  
  
-   可以从测试项目的上下文菜单开始项目升级。  
  
    在某些情况下，SQL Server Data Tools 将不显示可以从中启动测试项目升级的对话框。  
  
-   升级项目时，将删除对较旧数据库测试框架的程序集引用并添加对新框架的引用和一个适配器程序集。 还将更新 app.config 文件。  
  
    > [!NOTE]  
    > 如果你的测试项目同时具有 DatabaseSetup 和 SQLDatabaseSetup 代码文件，将项目升级到 SQL Server Data Tools 时将会从生成中排除 DatabaseSetup 文件。 如果从生成中排除 DatabaseSetup 文件，您可以删除它。  
  
-   转换后，使用较旧模板创建的现有数据库单元测试将使用适配器程序集中的类型来访问新框架。 适配器程序集的使用意味着升级过程不修改您的测试脚本和代码。 如果将 SQL Server 单元测试添加到项目，新测试将直接引用新框架而不通过适配器引用。 您可以选择手动更新现有代码来使用新框架以与新测试保持一致，但是不是必须这样做。  
  
## <a name="see-also"></a>另请参阅  
[使用 SQL Server 单元测试验证数据库代码](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
