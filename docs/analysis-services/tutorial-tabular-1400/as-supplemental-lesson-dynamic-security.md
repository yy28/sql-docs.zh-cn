---
title: Analysis Services 教程补充课程：动态安全性 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 81d2c60f281e439b010b8ead087e13cafa91c95e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "67149001"
---
# <a name="supplemental-lesson---dynamic-security"></a>补充课程 - 动态安全性

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本补充课程中，您可以创建实现动态安全性的其他角色。 动态安全性提供了基于当前登录用户的用户名或登录 ID 的行级别安全性。 
  
若要实现动态安全性，您将表添加到您的模型包含那些可以连接到模型并浏览模型对象和数据的用户的用户名。 使用本教程创建的模型是 Adventure Works; 的上下文中但是，若要完成本课程中，必须添加一个包含来自自己域的用户表。 添加的用户名称不需要的密码。 若要使用您自己域的用户的小型示例创建 EmployeeSecurity 表，您使用粘贴功能粘贴 Excel 电子表格中的员工数据。 在实际方案中，包含用户名的表通常是实际数据库中的表作为数据源;例如，实际的 DimEmployee 表。  
  
若要实现动态安全性，您可以使用两个 DAX 函数：[USERNAME 函数 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)并[LOOKUPVALUE 函数 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)。 这两个函数在新角色中进行定义，应用在行筛选器公式中。 通过使用 LOOKUPVALUE 函数，该公式指定 EmployeeSecurity 表中的值。 公式随后将传递给 USERNAME 函数，后者指定登录的用户的用户名的值属于此角色。 然后，用户可以浏览仅指定的角色的行筛选器的数据。 在此方案中，您指定销售员工只能浏览的成员的销售区域的 Internet 销售数据。  
  
这些任务是此 Adventure Works 表格模型方案所特有的，但并不一定适用于实际的应用场景。 每个任务都包含描述任务目的的附加信息。  
  
估计的时间才能完成本课程中：**30 分钟**  
  
## <a name="prerequisites"></a>先决条件  

本文补充课程是表格建模教程应按顺序完成的一部分。 在执行本补充课程中的任务之前，您应已完成所有之前的课程。  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>将 dimSalesTerritory 表添加到 AW Internet Sales 表格模型项目中  

若要实现动态安全性为此 Adventure Works 方案，必须将另外两个表添加到您的模型中。 添加的第一个表是来自同一 AdventureWorksDW 数据库的 DimSalesTerritory （作为 Sales Territory)。 更高版本到定义已登录用户可以浏览的特定数据在 SalesTerritory 表应用行筛选器。  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>添加 dimSalesTerritory 表  
  
1.  在表格模型资源管理器 >**数据源**，右键单击您的连接，并单击**导入新表**。  

    如果出现模拟凭据对话框中，键入在第 2 课中所使用的模拟凭据：添加数据。
  
2.  在导航器中，选择**DimSalesTerritory**表，并单击**确定**。    
  
3.  在查询编辑器中，单击**DimSalesTerritory**查询，然后删除**SalesTerritoryAlternateKey**列。  
  
7.  单击“导入”  。  
  
    新表添加到模型工作区中。 对象和源 DimSalesTerritory 表中的数据然后导入 AW Internet Sales 表格模型。  
  
9. 已成功导入表后，单击**关闭**。  

## <a name="add-a-table-with-user-name-data"></a>向表中添加用户名数据  

AdventureWorksDW 示例数据库中的 DimEmployee 表包含来自 AdventureWorks 域的用户。 在您自己的环境中不存在这些用户名。 必须包含少量示例 （至少三个） 的实际用户的组织在模型中创建一个表。 然后将这些用户作为成员添加到新的角色。 不需要示例用户名的密码，但从你自己的域需要实际 Windows 用户名。  
  
#### <a name="to-add-an-employeesecurity-table"></a>若要添加 EmployeeSecurity 表  
  
1.  打开 Microsoft Excel 并创建一个工作表。  
  
2.  复制下面的表（包括标题行），然后将其粘贴到该工作表中。  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  替换为名字、 姓氏和 domain\username 的名称和你的组织中的三个用户的登录 id。 对于 EmployeeId 1，表明此用户属于多个销售区域的前两个行添加相同的用户。 将 EmployeeId 和 SalesTerritoryId 字段保留原样。  
  
4.  保存的工作表**SampleEmployee**。  
  
5.  在工作表中，选择包含员工数据，包括标头，所有单元格，然后右键单击所选的数据，然后依次**复制**。  
  
6.  在 SSDT 中，单击**编辑**菜单，并单击**粘贴**。  
  
    如果粘贴灰显，单击模型设计器窗口中的任何表中的任何列，然后重试。  
  
7.  在中**粘贴预览**对话框中**表名**，类型**EmployeeSecurity**。  
  
8.  在中**要粘贴的数据**，确认数据包含的所有用户数据和从 SampleEmployee 工作表的标头。  
  
9. 确认已选中“使用第一行作为列标题”  ，然后单击“确定”  。  
  
    创建包含从 SampleEmployee 工作表复制的员工数据命名 EmployeeSecurity 的新表。  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>FactInternetSales、 DimGeography 和 DimSalesTerritory 表之间创建关系  

所有 FactInternetSales、 DimGeography 和 DimSalesTerritory 表都包含通用列 SalesTerritoryId。 DimSalesTerritory 表中的 SalesTerritoryId 列包含每个销售区域不同的 Id 值。  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a>若要创建 FactInternetSales、 DimGeography 和 DimSalesTerritory 表之间的关系  
  
1.  在关系图视图中，在**DimGeography**表，单击并按住**SalesTerritoryId**列，然后光标拖到**SalesTerritoryId**中列**DimSalesTerritory**表，然后松开。  
  
2.  在中**FactInternetSales**表，单击并按住**SalesTerritoryId**列，然后光标拖到**SalesTerritoryId**中的列**DimSalesTerritory**表，然后松开。  
  
    请注意，此关系的 Active 属性为 False，这意味着它处于非活动状态。 在 FactInternetSales 表已有另一个活动关系。  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>隐藏 EmployeeSecurity 表客户端应用程序  

在此任务中，您隐藏 EmployeeSecurity 表，防止它显示在客户端应用程序的字段列表中。 请注意，隐藏某个表不保证其安全。 用户仍可以查询 EmployeeSecurity 表数据，如果他们知道如何。 若要保护 EmployeeSecurity 表数据，防止用户能够查询其数据的任何您应用更高版本的任务中的筛选器。  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>若要隐藏 EmployeeSecurity 表客户端应用程序  
  
-   在模型设计器的“关系图视图”中，右键单击“Employee”  表标题，然后单击“从客户端工具中隐藏”  。  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>创建 Sales Employees by Territory 用户角色  

在此任务中，您可以创建用户角色。 此角色包括定义 DimSalesTerritory 表中的哪些行对用户可见的行筛选器。 一个对多关系的方向与 DimSalesTerritory 相关的所有其他表，然后应用筛选器。 您还可以应用筛选器来保护整个 EmployeeSecurity 表无法查询的任何用户角色的成员。  
  
> [!NOTE]  
> 您在本课程中创建的 Sales Employees by Territory 角色将限制成员只浏览（或查询）其所属的销售区域的销售数据。 如果你将用户添加为成员为 Sales Employees by Territory 角色也存在于角色的成员在创建[第 11 课：创建角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)，获得权限组合。 在某一用户是多个角色的成员时，为每个角色定义的权限和行筛选器将累积。 也就是说，用户具有角色的组合确定的更高权限。  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>创建 Sales Employees by Territory 用户角色  
  
1.  在 SSDT 中，单击**模型**菜单，并单击**角色**。  
  
2.  在中**角色管理器**，单击**新建**。  
  
    一个具有“无”权限的新角色将添加到列表中。  
  
3.  单击新角色，然后在**名称**列中，重命名为**Sales Employees by Territory**。  
  
4.  在“权限”  列中，单击下拉列表，然后选择“读取”  权限。  
  
5.  单击**成员**选项卡，然后依次**添加**。  
  
6.  在中**选择用户或组**对话框中**输入要选择的对象名称**，键入创建 EmployeeSecurity 表时使用的第一个示例用户名。 单击“检查名称”  以确认该用户名有效，然后单击“确定”  。  
  
    重复此步骤中，添加创建 EmployeeSecurity 表时所用的其他示例用户名称。  
  
7.  单击**行筛选器**选项卡。  
  
8.  有关**EmployeeSecurity**表，在**DAX 筛选器**列中，键入以下公式：  
  
    ```
      =FALSE()  
    ```
  
    此公式指定所有列均都解析为 false 布尔条件。 By Territory 用户角色，销售员工的成员可以不查询 EmployeeSecurity 表中的任何列。  
  
9. 有关**DimSalesTerritory**表中，键入以下公式：  

    ```  
    ='DimSalesTerritory'[SalesTerritoryKey]=LOOKUPVALUE('EmployeeSecurity'[SalesTerritoryId], 
      'EmployeeSecurity'[LoginId], USERNAME(), 
      'EmployeeSecurity'[SalesTerritoryId], 'DimSalesTerritory'[SalesTerritoryKey]) 
    ```
  
    在此公式中，LOOKUPVALUE 函数返回 DimEmployeeSecurity [SalesTerritoryId] 列，其中，EmployeeSecurity [LoginId] 是与当前登录的 Windows 用户名相同，EmployeeSecurity [SalesTerritoryId] 是的所有值与 DimSalesTerritory [SalesTerritoryId] 相同。  
  
    然后使用 lookupvalue 返回的 Id 的销售区域组来限制 DimSalesTerritory 表中所示的行。 显示仅行 SalesTerritoryID 在 LOOKUPVALUE 函数返回的 Id 集中的所在的行。  
  
10. 在角色管理器中，单击**确定**。  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>测试 Sales Employees by Territory 用户角色  

在此任务中，您使用分析在 Excel 功能在 SSDT 中测试的效用 Sales Employees by Territory 用户角色。 需要指定一个添加到 EmployeeSecurity 表和角色的成员的用户名称。 作为创建 Excel 与模型之间的连接中的有效用户名称，然后使用此用户名。  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>测试 Sales Employees by Territory 用户角色  
  
1.  在 SSDT 中，单击**模型**菜单，并单击**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”  对话框的“指定用于连接到模型的用户名或角色”  中，选择“其他 Windows 用户”  ，然后单击“浏览”  。  
  
3.  在中**选择用户或组**对话框中**输入要选择的对象名称**，键入用户名称包含在 EmployeeSecurity 表，然后单击**检查名称**。  
  
4.  单击“确定”  关闭“选择用户或组”  对话框，然后单击“确定”  关闭“在 Excel 中分析”  对话框。  
  
    Excel 中打开新的工作簿。 自动创建数据透视表。 数据透视表字段列表包含新模型中可用的数据字段的大多数。  
  
    请注意，EmployeeSecurity 表不在数据透视表字段列表中可见。 隐藏此表从上一任务中的客户端工具。  
  
5.  在中**字段**列表中，在**∑ Internet Sales** （度量值），选择**InternetTotalSales**度量值。 度量值输入到**值**字段。  
  
6.  选择**SalesTerritoryId**中的列**DimSalesTerritory**表。 该列输入到**行标签**字段。  
  
    请注意，仅显示您使用的有效用户名所属的一个区域的 Internet 销售数字。 如果选择另一列，如城市从 DimGeography 表作为行标签字段，将显示仅有效用户所属销售区域中的城市。  
    此用户无法浏览或查询不是其所属的区域任何 Internet 销售数据。 此限制是因为针对 DimSalesTerritory 表中的，销售员工 by Territory 用户角色中保护的与其他销售区域相关的所有数据定义行筛选器。  
  
## <a name="see-also"></a>请参阅  

[USERNAME 函数 (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE 函数 (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA 函数 (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  
