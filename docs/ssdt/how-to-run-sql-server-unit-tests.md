---
title: 如何：运行 SQL Server 单元测试 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 34fe2d1e-d47b-4808-af56-8cc0fdae6518
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b838503365dde968f938efb46c940f3a66ce4357
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098460"
---
# <a name="how-to-run-sql-server-unit-tests"></a>如何：运行 SQL Server 单元测试
可以通过多种方式之一运行 SQL Server 单元测试，例如使用各种窗口和命令提示符窗口。  
  
> [!NOTE]  
> 不能远程运行单元测试。  
  
如[运行 SQL Server 单元测试](../ssdt/running-sql-server-unit-tests.md)中所述，可供你使用的方式取决于你所安装的软件。  
  
### <a name="to-run-sql-server-unit-tests-using-test-view-visual-studio-2010"></a>使用测试视图运行 SQL Server 单元测试 (Visual Studio 2010)  
  
1.  在“测试”  菜单上，指向“窗口”  ，然后单击“测试视图”  。  
  
    此时将打开“测试视图”  窗口。  
  
2.  在“测试视图”  窗口中，单击要运行的一个或多个测试。 通过使用 Ctrl 键或 Shift 键，您可以指定一组不连续或连续的测试。  
  
3.  执行下列任一操作：  
  
    -   右键单击“测试视图”  窗口界面，然后单击“运行选定内容”  。  
  
    -   在“测试视图”  工具栏中，单击“运行选定内容”  。  
  
### <a name="to-run-sql-server-unit-tests-using-test-explorer-visual-studio-2012"></a>使用测试资源管理器运行 SQL Server 单元测试 (Visual Studio 2012)  
  
1.  在“测试”  菜单上，指向“窗口”  ，然后单击“测试资源管理器”  。  
  
    此时将打开“测试资源管理器”  窗口。  
  
2.  在“测试资源管理器”  中，单击要运行的一个或多个测试。 通过使用 Ctrl 键或 Shift 键，您可以指定一组不连续或连续的测试。  
  
3.  右键单击突出显示的测试之一，然后单击“运行选定测试”  。  
  
### <a name="to-run-sql-server-unit-tests-from-the-sql-server-unit-test-designer-visual-studio-2010"></a>从 SQL Server 单元测试设计器中运行 SQL Server 单元测试 (Visual Studio 2010)  
  
-   在“测试工具”  工具栏上，你将找到使用和不带调试器启动项目的按钮。  
  
此步骤会运行当前测试运行中的所有测试。 启动测试运行后，“测试结果”  窗口将出现并显示测试运行的进度。 此显示内容包括正在运行的测试和已完成的测试。 有关详细信息，请参阅[解释 SQL Server 单元测试结果](../ssdt/interpreting-sql-server-unit-test-results.md)。  
  
## <a name="see-also"></a>另请参阅  
[运行 SQL Server 单元测试](../ssdt/running-sql-server-unit-tests.md)  
[如何：从 Microsoft Visual Studio 2010 运行自动测试](https://msdn.microsoft.com/library/ms182470(VS.100).aspx)  
[从命令行运行自动化测试 (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182486(VS.100).aspx)  
[测试应用程序 (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182409.aspx)  
  
