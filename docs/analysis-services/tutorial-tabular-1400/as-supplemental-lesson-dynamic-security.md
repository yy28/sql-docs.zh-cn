---
title: Analysis Services 教程补充课程： 动态安全性 |Microsoft 文档
description: 描述如何通过在 Analysis Services 教程中使用行筛选器来使用动态安全性。
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: ffd58456ee40741792ac7ce409c97e064a92ba43
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="supplemental-lesson---dynamic-security"></a>补充课程-动态安全性

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在此补充课程中，你将创建实现动态安全性的其他角色。 动态安全性提供了基于当前登录用户的用户名或登录 ID 的行级别安全性。 
  
若要实现动态安全性，你将表添加到你的模型包含的那些可以连接到模型和浏览模型对象和数据的用户的用户名。 使用本教程创建的模型是 Adventure Works; 的上下文中但是，若要完成本课程中，必须添加一个包含从你自己的域的用户表。 添加的用户名称不需要密码。 若要创建一个 EmployeeSecurity 表，使用你自己的域中的用户列表小示例，你使用粘贴功能中，粘贴从 Excel 电子表格的员工数据。 在实际方案中，包含用户名的表通常是实际的数据库中的表作为数据源，则例如，实际的 DimEmployee 表。  
  
若要实现动态安全性，你可以使用两个 DAX 函数：[用户名函数 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)和[LOOKUPVALUE 函数 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)。 这两个函数在新角色中进行定义，应用在行筛选器公式中。 通过使用 LOOKUPVALUE 函数，该公式指定 EmployeeSecurity 表中的值。 该公式随后将传递给用户名函数，这样指定登录的用户的用户名的值属于此角色。 之后，该用户只能浏览此角色的行筛选器指定的数据。 在此方案中，你可以指定销售员工只能浏览 Internet 它们是成员的销售区域的销售数据。  
  
这些任务是此 Adventure Works 表格模型方案所特有的，但并不一定适用于实际的应用场景。 每个任务都包含描述任务目的的附加信息。  
  
学完本课的估计时间： **30 分钟**  
  
## <a name="prerequisites"></a>必要條件  

补充课程本文摘自表格建模教程中，应按顺序完成。 在执行本补充课程中的任务之前，您应已完成所有之前的课程。  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>将 dimSalesTerritory 表添加到 AW Internet Sales 表格模型项目中  

若要实现此方案中 Adventure Works 的动态安全性，必须将两个其他表添加到你的模型中。 你添加的第一个表是从相同的 AdventureWorksDW 数据库 DimSalesTerritory （作为销售区域）。 稍后将行筛选器应用到的 SalesTerritory 表中定义的登录的用户可以浏览的特定数据。  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>添加 dimSalesTerritory 表  
  
1.  在表格模型资源管理器 >**数据源**，右键单击你的连接，，然后单击**导入新表**。  

    如果出现“模拟凭据”对话框，请键入您在“第 2 课：添加数据”中使用的模拟凭据。
  
2.  在导航器中，选择**DimSalesTerritory**表，并依次**确定**。    
  
3.  在查询编辑器中，单击**DimSalesTerritory**查询，，然后删除**SalesTerritoryAlternateKey**列。  
  
7.  单击“导入” 。  
  
    新表添加到模型工作区中。 对象和数据从源表 DimSalesTerritory 然后导入 AW Internet 销售表格模型。  
  
9. 已成功导入表后，单击**关闭**。  

## <a name="add-a-table-with-user-name-data"></a>向表中添加用户名数据  

AdventureWorksDW 示例数据库中的 DimEmployee 表包含 AdventureWorks 域中的用户。 你自己的环境中不存在这些用户名称。 必须包含小型 （至少三个） 的示例从你的组织的实际用户在模型中创建一个表。 然后将这些用户作为成员添加到新的角色。 示例用户名称，不需要密码，但你从你自己的域需要实际的 Windows 用户名。  
  
#### <a name="to-add-an-employeesecurity-table"></a>若要添加 EmployeeSecurity 表  
  
1.  打开 Microsoft Excel 中，创建一个工作表。  
  
2.  复制下面的表（包括标题行），然后将其粘贴到该工作表中。  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  将替换的名称和你组织中的三个用户的登录 id 的名字、 姓氏和域 \ 用户名。 对于 EmployeeId 1，显示此用户属于多个销售区域放的前两行，同一个用户。 将 EmployeeId 和 SalesTerritoryId 字段保留原样。  
  
4.  保存该工作表作为**SampleEmployee**。  
  
5.  在工作表中，选择员工数据，包括标头，具有的所有单元格，然后右键单击所选的数据，并依次**复制**。  
  
6.  在 SSDT 中，单击**编辑**菜单，，然后单击**粘贴**。  
  
    如果粘贴灰显，则单击在模型设计器窗口中，任何表中的任何列，然后重试。  
  
7.  在**粘贴预览**对话框中，在**表名**，类型**EmployeeSecurity**。  
  
8.  在**要粘贴的数据**，验证的数据包括所有的用户数据和从 SampleEmployee 表中的标头。  
  
9. 确认已选中“使用第一行作为列标题”，然后单击“确定”。  
  
    创建命名 EmployeeSecurity 从 SampleEmployee 工作表复制的员工数据的新表。  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>创建 FactInternetSales、 DimGeography 和 DimSalesTerritory 表之间的关系  

所有 FactInternetSales、 DimGeography 和 DimSalesTerritory 表包含常见的列，SalesTerritoryId。 DimSalesTerritory 表中的 SalesTerritoryId 列包含与每个销售区域的不同 Id 的值。  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a>若要创建 FactInternetSales、 DimGeography 和 DimSalesTerritory 表之间的关系  
  
1.  在关系图视图中**DimGeography**表，单击并按住上**SalesTerritoryId**列，然后拖动光标所在位置到**SalesTerritoryId**中的列**DimSalesTerritory**表，，然后释放。  
  
2.  在**FactInternetSales**表，单击并按住上**SalesTerritoryId**列，然后拖动光标所在位置到**SalesTerritoryId**中的列**DimSalesTerritory**表，，然后释放。  
  
    请注意此关系的 Active 属性为 False 时，这意味着它处于非活动状态。 FactInternetSales 表已经有另一个活动关系。  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>隐藏 EmployeeSecurity 表从客户端应用程序  

在此任务中，则隐藏 EmployeeSecurity 表中，阻止将其显示在客户端应用程序的字段列表中。 请记住，隐藏表不会保护它。 如果他们知道，用户仍然可以查询 EmployeeSecurity 表数据如何。 若要保护 EmployeeSecurity 表数据，防止用户来查询任何数据，你应用中更高版本的任务的筛选器。  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>若要隐藏 EmployeeSecurity 表从客户端应用程序  
  
-   在模型设计器的“关系图视图”中，右键单击“Employee”表标题，然后单击“从客户端工具中隐藏”。  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>创建 Sales Employees by Territory 用户角色  

在此任务中，你可以创建用户角色。 此角色包括行筛选器定义中对用户可见的 DimSalesTerritory 表的行。 一个对多关系方向与 DimSalesTerritory 与相关的所有其他表，然后应用筛选器。 你还可以应用筛选器保护整个 EmployeeSecurity 表从正在查询的任何用户都是角色的成员。  
  
> [!NOTE]  
> 您在本课程中创建的 Sales Employees by Territory 角色将限制成员只浏览（或查询）其所属的销售区域的销售数据。 如果你将用户添加为成员销售人员才有权通过也存在在创建角色的成员的区域角色[课 11： 创建角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)，获取权限的组合。 在某一用户是多个角色的成员时，为每个角色定义的权限和行筛选器将累积。 也就是说，用户具有较高的权限由角色的组合。  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>创建 Sales Employees by Territory 用户角色  
  
1.  在 SSDT 中，单击**模型**菜单，，然后单击**角色**。  
  
2.  在**角色管理器**，单击**新建**。  
  
    一个具有“无”权限的新角色将添加到列表中。  
  
3.  单击新的角色，然后在**名称**列中，重命名该角色向**按地区的销售员工**。  
  
4.  在“权限”列中，单击下拉列表，然后选择“读取”权限。  
  
5.  单击**成员**选项卡上，并依次**添加**。  
  
6.  在**选择用户或组**对话框中，在**输入名为选择的对象**，键入你在创建 EmployeeSecurity 表时使用的第一个示例用户名。 单击“检查名称”以确认该用户名有效，然后单击“确定”。  
  
    重复此步骤中，添加创建 EmployeeSecurity 表时使用的其他示例用户名称。  
  
7.  单击**行筛选器**选项卡。  
  
8.  有关**EmployeeSecurity**表中， **DAX 筛选器**列中，键入以下公式：  
  
    ```
      =FALSE()  
    ```
  
    此公式指定所有列均都解析为 false 布尔条件。 按区域用户角色，销售员工的成员可以查询 EmployeeSecurity 表没有列。  
  
9. 有关**DimSalesTerritory**表中，键入以下公式：  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    此公式中，使用 LOOKUPVALUE 函数返回 DimEmployeeSecurity [SalesTerritoryId] 列，其中 EmployeeSecurity [LoginId] 是与当前登录的 Windows 用户名称相同，EmployeeSecurity [SalesTerritoryId] 等同于 DimSalesTerritory [SalesTerritoryId] 的所有值。  
  
    然后使用 LOOKUPVALUE 所返回的 Id 的销售区域集来限制 DimSalesTerritory 表所示的行。 只有 LOOKUPVALUE 函数返回的 Id 集的行 SalesTerritoryID 所在的行才会显示。  
  
10. 在角色管理器中，单击**确定**。  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>测试 Sales Employees by Territory 用户角色  

在此任务中，你用于分析在 SSDT 中的 Excel 功能中测试销售员工的效用按区域用户角色。 你指定的用户名，你添加到 EmployeeSecurity 表，并为角色的成员之一。 作为创建 Excel 与模型之间的连接中的有效用户名称，然后使用此用户名。  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>测试 Sales Employees by Territory 用户角色  
  
1.  在 SSDT 中，单击**模型**菜单，，然后单击**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”对话框的“指定用于连接到模型的用户名或角色”中，选择“其他 Windows 用户”，然后单击“浏览”。  
  
3.  在**选择用户或组**对话框中，在**输入要选择的对象名称**，键入 EmployeeSecurity 表中包含的用户名称，然后单击**检查名称**。  
  
4.  单击“确定”关闭“选择用户或组”对话框，然后单击“确定”关闭“在 Excel 中分析”对话框。  
  
    Excel 将打开与新的工作簿。 自动创建数据透视表。 数据透视表字段列表包括大多数新模型中可用的数据字段。  
  
    请注意 EmployeeSecurity 表不在数据透视表字段列表中可见。 隐藏此表上一任务中的客户端工具。  
  
5.  在**字段**列表中， **∑ Internet Sales** （度量值），选择**InternetTotalSales**度量值。 度量值输入到**值**字段。  
  
6.  选择**SalesTerritoryId**列从**DimSalesTerritory**表。 列输入到**行标签**字段。  
  
    请注意，仅显示您使用的有效用户名所属的一个区域的 Internet 销售数字。 如果选择另一列，如市/县从 DimGeography 表作为行标签字段，将显示仅有效用户属于销售区域中的城市。  
    此用户无法浏览或查询不是它们属于区域的任何 Internet 销售数据。 此限制是因为行筛选器定义为 DimSalesTerritory 表，在由区域用户角色，销售员工保护的数据与其他销售区域相关的所有数据。  
  
## <a name="see-also"></a>另请参阅  

[USERNAME 函数 (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE 函数 (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA 函数 (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  
