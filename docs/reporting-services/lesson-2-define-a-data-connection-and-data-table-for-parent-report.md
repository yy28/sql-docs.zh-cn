---
title: 第 2 课：定义用于父报表的数据连接和数据表 | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e8bcfe976a8094c6faa22d8aab3db8a4a833d8cd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "62651595"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>第 2 课：定义用于父报表的数据连接和数据表
使用 Visual C# 的 ASP.NET 网站模板创建新网站项目后，接下来要创建用于父报表的数据连接和数据表。 在本教程中，数据连接指向 AdventureWorks2014 数据库。  
  
## <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>通过添加 DataSet 定义数据连接和 DataTable（用于父报表）  
  
1.  在“网站”菜单上，选择“添加新项”   。  
  
2.  在“添加新项”对话框中，选择“数据集”，然后选择“添加”    。 出现提示后，应选择“是”，将该项添加到 App_Code 文件夹   。  
  
    此操作会将一个新的 XSD 文件 **DataSet1.xsd** 添加到项目，然后打开数据集设计器。  
  
3.  从“工具箱”窗口中，将一个 **[TableAdapter](/visualstudio/data-tools/fill-datasets-by-using-tableadapters)** 控件拖到设计图面上。 随后将启动 **TableAdapter** 配置向导。  
  
4.  在“选择你的数据连接”页上，选择“新建连接”   。  
  
5.  如果是首次在 Visual Studio 中创建数据源，可看到“选择数据源”页  。 在“数据源”框中，选择“Microsoft SQL Server”   。  
  
6.  在“添加连接”对话框中，执行以下步骤  ：  
  
    1.  在“服务器名称”框中，输入 AdventureWorks2014 数据库所在的服务器   。  
  
        默认的 SQL Server Express 实例为 **(local)\sqlexpress**。  
  
    2.  在“登录到服务器”部分中，选择使你可访问数据的选项  。 “使用 Windows 身份验证”为默认选项  。  
  
    3.  在“选择或输入数据库名称”下拉列表中，选择“AdventureWorks2014”   。  
  
    4.  选择“确定”  ，然后选择“下一步”  。  
  
7.  如果在第 6 (b) 步中选择了“使用 SQL Server 身份验证”，则选择一个选项，决定是在字符串中加入敏感数据还是在应用程序代码中设置该信息  。  
  
8.  在“将连接字符串保存到应用程序配置文件中”页上，键入连接字符串的名称，或接受默认的“AdventureWorks2014ConnectionString”   。 选择“**下一页**”。  
  
9. 在“选择命令类型”页上，选择“使用 SQL 语句”，然后选择“下一步”    。  
  
10. 在“输入 SQL 语句”页上，输入以下 Transact-SQL 查询以从 AdventureWorks2014 数据库检索数据，然后选择“下一步”    。  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
    还可通过选择“查询生成器”创建查询，然后通过选择“执行查询”验证查询   。 如果查询返回的数据不符合预期，则可能使用的 AdventureWorks 版本较低。 有关如何获取 AdventureWorks2014 示例数据库的详细信息，请参阅 [AdventureWorks sample databases](https://github.com/Microsoft/sql-server-samples/releases)  （AdventureWorks 示例数据库）。  
  
11. 在“选择要生成的方法”页上，务必取消选中“创建方法以将更新直接发送到数据库(GenerateDBDirectMethods)”，然后选择“完成”    。  
  
    > [!WARNING]  
    > 务必取消选中“创建方法以将更新直接发送到数据库(GenerateDBDirectMethods)”   
  
    配置 ADO.NET DataTable 对象作为报表的数据源现已完毕。 在 Visual Studio 中的“数据集设计器”页上，应看到所添加的 DataTable 对象，并列出在查询中指定的列。 DataSet1 由根据查询从 Product 表获得的数据组成。  
  
12. 保存文件。  
  
13. 要预览数据，请在“数据”菜单上选择“预览数据”，然后选择“预览”    。  
  
## <a name="next-task"></a>下一个任务  
您已成功创建了用于父报表的数据连接和数据表。 接下来，将使用报表向导设计父报表。 请参阅[第 3 课：使用报表向导设计父报表](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)。  
  

