---
title: 第 4 课：定义用于子报表的数据连接和数据表 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c1008202519f1d9bcbf48dfdc4cd4ef3a3cbbe20
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108466"
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>第 4 课：定义用于子报表的数据连接和数据表
  设计父报表后，接下来要创建用于子报表的数据连接和数据表。 在本教程中，数据连接指向 AdventureWorks2008 数据库。 也可选择连接到 AdventureWorks2012 数据库。  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>通过添加 DataSet 定义数据连接和 DataTable（用于子报表）  
  
1.  在 "**网站**" 菜单上，单击 "**添加新项**"。  
  
2.  在 "**添加新项**" 对话框中，单击 "**数据集**"，然后单击 "**添加**"。 出现提示时，应通过单击 **"是"** 将该项添加到**App_Code**文件夹。  
  
     此操作将一个新的 XSD 文件 **DataSet2.xsd** 添加到项目，并打开数据集设计器。  
  
3.  从“工具箱”窗口中，将一个 **TableAdapter** 控件拖到设计图面上。 随后将启动 **TableAdapter** 配置向导。  
  
4.  在 "**选择你的数据连接**" 页上，单击 "**新建连接**"。  
  
5.  在“添加连接”对话框中，执行以下步骤****：  
  
    1.  在 "**服务器名称**" 框中，输入**AdventureWorks2008**数据库所在的服务器。  
  
         默认的 SQL Server Express 实例为 **(local)\sqlexpress**。  
  
    2.  在“登录到服务器”部分中，选择使你可访问数据的选项****。 “使用 Windows 身份验证”为默认选项****。  
  
    3.  在 "**选择或输入数据库名称**" 下拉列表中，单击 " **AdventureWorks2008**"。  
  
    4.  单击 **“确定”**，然后单击 **“下一步”**。  
  
6.  如果在步骤 5 (b) 中选择了“使用 SQL Server 身份验证”，则选择一个选项，决定是在字符串中加入敏感数据还是在应用程序代码中设置该信息****。  
  
7.  在 "将**连接字符串保存到应用程序配置文件**中" 页上，键入连接字符串的名称，或接受默认的**AdventureWorks2008ConnectionString**。 单击“下一步”  。  
  
8.  在 "**选择命令类型**" 页上，选择 "**使用 SQL 语句**"，然后单击 "**下一步**"。  
  
9. 在 "**输入 SQL 语句**" 页上，输入以下 transact-sql 查询以从**AdventureWorks2008**数据库检索数据，然后单击 "**下一步**"。  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
     还可以通过单击 "**查询生成器**" 创建查询，然后通过单击 "**执行查询**" 按钮验证查询。 如果查询返回的数据不符合预期，则可能使用的 AdventureWorks 版本较低。 有关安装 AdventureWorks 的**AdventureWorks2008**版本的详细信息，请参阅[演练：安装 adventureworks 数据库](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx)。  
  
10. 在 "**选择要生成的方法**" 页上，取消选中 **"创建方法以将更新直接发送到数据库（GenerateDBDirectMethods）**"，然后单击 "**完成**"。  
  
     现在已完成将 ADO.NET [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx)配置为报表的数据源。 在 Visual Studio 中的“数据集设计器”页上，应看到所添加的 **DataTable** ，其中列出在查询中指定的列。 DataSet2 由根据查询从 PurhcaseOrderDetail 表获得的数据组成。  
  
11. 保存该文件。  
  
12. 若要预览数据，请在 "**数据**" 菜单上单击 "**预览数据**"，然后单击 "**预览**"。  
  
## <a name="next-task"></a>下一个任务  
 您已成功创建了用于子报表的数据连接和数据表。 接下来，将使用报表向导设计子报表。  
  
  
