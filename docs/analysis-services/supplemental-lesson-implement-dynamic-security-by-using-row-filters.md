---
title: 通过使用行筛选器实现动态安全性 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 715d3b06ed3017a00852f58c618e2ea0b0de24d8
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403342"
---
# <a name="supplemental-lesson---implement-dynamic-security-by-using-row-filters"></a>补充课程-通过使用行筛选器实现动态安全性
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本补充课程中，您将另外创建一个实现动态安全性的角色。 动态安全性提供了基于当前登录用户的用户名或登录 ID 的行级别安全性。 若要了解详细信息，请参阅[角色](../analysis-services/tabular-models/roles-ssas-tabular.md)。  
  
若要实现动态安全性，您必须向模型中添加一个表，该表中包含那些可以创建与模型的连接作为数据源并可浏览模型对象和数据的用户的 Windows 用户名。 您使用本教程创建的模型位于 Adventure Works Corp. 上下文中；但是，若要完成本课程，您必须添加一个表，其中包含来自您自己域的用户。 您不需要将添加的用户名的密码。 若要使用您自己域的用户的小型示例创建 EmployeeSecurity 表，将使用粘贴功能粘贴 Excel 电子表格中的员工数据。 在实际应用场景中，包含添加到模型中的用户名的表通常将使用实际数据库中的表作为数据源；例如，实际的 dimEmployee 表。  
  
为了实现动态安全性，您将使用两个新的 DAX 函数：[USERNAME 函数 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)并[LOOKUPVALUE 函数 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)。 这两个函数在新角色中进行定义，应用在行筛选器公式中。 该公式使用 LOOKUPVALUE 函数，指定 EmployeeSecurity 表中的值，并随后将传递给 USERNAME 函数，后者指定登录的用户的用户名的值属于此角色。 然后，用户可以浏览仅指定的角色的行筛选器的数据。 在这种情况下，您将指定销售员工只能浏览自己为其中成员的销售区域的 Internet 销售数据。  
  
若要完成本补充课程，您将需要完成一系列任务。 这些任务是此 Adventure Works 表格模型方案所特有的，但并不一定适用于实际的应用场景。 每个任务都包含描述任务目的的附加信息。  
  
学完本课的预计时间：**30 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本补充课程主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本补充课程中的任务之前，您应已完成所有之前的课程。  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>将 dimSalesTerritory 表添加到 AW Internet Sales 表格模型项目中  
若要为此 Adventure Works 方案实现动态安全性，您必须向模型中另外添加两个表。 第一个要添加的表是来自同一 AdventureWorksDW 数据库的 dimSalesTerritory（作为 Sales Territory）。 更高版本将于定义已登录用户可以浏览的特定数据的 SalesTerritory 表应用行筛选器。  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>添加 dimSalesTerritory 表  
  
1.  在 SSDT 中，单击**模型**菜单，并单击**现有连接**。  
  
2.  在“现有连接”对话框中，确认已选中“Adventure Works DB from SQL”数据源连接，然后单击“打开”。  
  
    如果出现模拟凭据对话框中，键入在第 2 课中所使用的模拟凭据：添加数据。  
  
3.  在“选择如何导入数据”页上，保持选中“从表和视图的列表中进行选择，以便选择要导入的数据”，然后单击“下一步”。  
  
4.  在“选择表和视图”页上，选择“DimSalesTerritory”表。  
  
5.  单击“预览并筛选”。  
  
6.  取消选择“SalesTerritoryAlternateKey”列，然后单击“确定”。  
  
7.  在“选择表和视图”页上，单击“完成”。  
  
    新表将添加到模型工作区中。 对象和源 DimSalesTerritory 表中的数据然后导入 AW Internet Sales 表格模型。  
  
9. 导入该表后，单击“关闭”。  

## <a name="add-a-table-with-user-name-data"></a>向表中添加用户名数据  
由于 AdventureWorksDW 示例数据库中的 dimEmployee 表包含来自 AdventureWorks 域的用户，而您自己的环境中不存在这些用户名，因此必须在您的模型中创建一个表，包含您组织中的少量实际示例用户（三个用户）。 然后，将这些用户作为成员添加到新角色中。 您不需要示例用户名的密码，但需要来自您自己域的实际 Windows 用户名。  
  
#### <a name="to-add-an-employeesecurity-table"></a>若要添加 EmployeeSecurity 表  
  
1.  打开 Microsoft Excel，创建一个新工作表。  
  
2.  复制下面的表（包括标题行），然后将其粘贴到该工作表中。  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  替换为名字、 姓氏和 domain\username 的名称和你的组织中的三个用户的登录 id。 对于 EmployeeId 1 上的前两行添加相同的用户。 这表示此用户属于多个销售区域。 将 EmployeeId 和 SalesTerritoryId 字段保留原样。  
  
4.  保存的工作表**SampleEmployee**。  
  
5.  在表中，选择所有单元格包含员工数据，包括标头，然后右键单击所选的数据，然后单击**复制**。  
  
6.  在 SSDT 中，单击**编辑**菜单，并单击**粘贴**。  
  
    如果粘贴灰显，单击模型设计器窗口中的任何表中的任何列，然后重试。  
  
7.  在中**粘贴预览**对话框中**表名**，类型**EmployeeSecurity**。  
  
8.  在中**要粘贴的数据**，确认数据包含的所有用户数据和从 SampleEmployee 工作表的标题。  
  
9. 确认已选中“使用第一行作为列标题”，然后单击“确定”。  
  
    创建包含从 SampleEmployee 工作表复制的员工数据命名 EmployeeSecurity 的新表。  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>FactInternetSales、 DimGeography 和 DimSalesTerritory 表之间创建关系  
所有 FactInternetSales、 DimGeography 和 DimSalesTerritory 表都包含通用列 SalesTerritoryId。 DimSalesTerritory 表中的 SalesTerritoryId 列包含每个销售区域不同的 Id 值。  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a>若要创建 FactInternetSales、 DimGeography 和 DimSalesTerritory 表之间的关系  
  
1.  在模型设计器中，在关系图视图中，在**DimGeography**表中，单击并按住**SalesTerritoryId**列，然后光标拖到**SalesTerritoryId**中的列**DimSalesTerritory**表，然后松开。  
  
2.  在中**FactInternetSales**表中，单击并按住**SalesTerritoryId**列，然后光标拖到**SalesTerritoryId**中的列**DimSalesTerritory**表，然后松开。  
  
    请注意，此关系的 Active 属性为 False，这意味着它处于非活动状态。 这是因为 FactInternetSales 表中已包含在度量值中使用的另一个活动关系。  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>隐藏 EmployeeSecurity 表客户端应用程序  
在本任务中，将隐藏 EmployeeSecurity 表，防止它显示在客户端应用程序的字段列表中。 请记住，隐藏表并不会保护表安全。 用户仍可以查询 EmployeeSecurity 表数据，如果他们知道如何。 若要保护 EmployeeSecurity 表数据，防止用户能够查询其任何数据，您将应用更高版本的任务中的筛选器。  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>若要隐藏 EmployeeSecurity 表客户端应用程序  
  
-   在模型设计器的“关系图视图”中，右键单击“Employee”表标题，然后单击“从客户端工具中隐藏”。  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>创建 Sales Employees by Territory 用户角色  
在此任务中，您将创建一个新的用户角色。 此角色将包含定义 DimSalesTerritory 表中的哪些行对用户可见的行筛选器。 一个对多关系的方向与 DimSalesTerritory 相关的所有其他表，然后应用筛选器。 您还将应用保护整个 EmployeeSecurity 表无法查询的任何用户角色的成员的简单筛选器。  
  
> [!NOTE]  
> 您在本课程中创建的 Sales Employees by Territory 角色将限制成员只浏览（或查询）其所属的销售区域的销售数据。 如果你将用户添加为成员为 Sales Employees by Territory 角色也存在于角色的成员在创建[第 11 课：创建角色](../analysis-services/lesson-11-create-roles.md)，您将获得权限组合。 在某一用户是多个角色的成员时，为每个角色定义的权限和行筛选器将累积。 也就是说，该用户将具有角色组合所确定的更大权限。  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>创建 Sales Employees by Territory 用户角色  
  
1.  在 SSDT 中，单击**模型**菜单，并单击**角色**。  
  
2.  在中**角色管理器**，单击**新建**。  
  
    一个具有“无”权限的新角色将添加到列表中。  
  
3.  单击新角色，然后在“名称”列中，将角色重命名为 **Sales Employees by Territory**。  
  
4.  在“权限”列中，单击下拉列表，然后选择“读取”权限。  
  
5.  单击“成员”选项卡，然后单击“添加”。  
  
6.  在中**选择用户或组**对话框中**输入要选择的对象名称**，键入创建 EmployeeSecurity 表时使用的第一个示例用户名。 单击“检查名称”以确认该用户名有效，然后单击“确定”。  
  
    重复此步骤中，添加创建 EmployeeSecurity 表时所用的其他示例用户名称。  
  
7.  单击“行筛选器”选项卡。  
  
8.  有关**EmployeeSecurity**表，在**DAX 筛选器**列中，键入以下公式。  
  
    ```
      =FALSE()  
    ```
  
    此公式指定所有列均都解析为 false 布尔条件;因此，可以 by Territory 用户角色的销售员工成员不查询 EmployeeSecurity 表中的任何列。  
  
9. 有关**DimSalesTerritory**表中，键入以下公式。  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    在此公式中，LOOKUPVALUE 函数返回 DimEmployeeSecurity [SalesTerritoryId] 列，其中，EmployeeSecurity [LoginId] 是与当前登录的 Windows 用户名相同，EmployeeSecurity [SalesTerritoryId] 是的所有值与 DimSalesTerritory [SalesTerritoryId] 相同。  
  
    然后使用 lookupvalue 返回的 Id 的销售区域组来限制 DimSalesTerritory 表中所示的行。 显示仅行 SalesTerritoryID 在 LOOKUPVALUE 函数返回的 Id 集中的所在的行。  
  
10. 在角色管理器中，单击**确定**。  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>测试 Sales Employees by Territory 用户角色  
在此任务中，你将在 SSDT 中的 Excel 功能中使用分析来测试效力 Sales Employees by Territory 用户角色。 将指定的用户名称添加到 EmployeeSecurity 表和角色的成员之一。 然后，此用户名将用作在 Excel 和模型之间创建的连接中的有效用户名。  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>测试 Sales Employees by Territory 用户角色  
  
1.  在 SSDT 中，单击**模型**菜单，并单击**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”对话框的“指定用于连接到模型的用户名或角色”中，选择“其他 Windows 用户”，然后单击“浏览”。  
  
3.  在中**选择用户或组**对话框中**输入要选择的对象名称**，键入一个包含在 EmployeeSecurity 表中的用户名称，然后单击**检查名称**.  
  
4.  单击“确定”关闭“选择用户或组”对话框，然后单击“确定”关闭“在 Excel 中分析”对话框。  
  
    Excel 将打开，并显示一个新工作簿。 自动创建数据透视表。 数据透视表字段列表包含新模型中可用的数据字段的大多数。  
  
    请注意，EmployeeSecurity 表不在数据透视表字段列表中可见。 这是因为您在前一任务中选择了从客户端工具隐藏此表。  
  
5.  在中**字段**列表中，在**∑ Internet Sales** （度量值），选择**InternetTotalSales**度量值。 该度量值将会输入到“值”字段中。  
  
6.  选择**SalesTerritoryId**中的列**DimSalesTerritory**表。 该列将会输入到“行标签”字段中。  
  
    请注意，仅显示您使用的有效用户名所属的一个区域的 Internet 销售数字。 如果选择另一列;例如，城市，作为行标签字段，仅有效用户所属销售区域中的城市 DimGeography 表中显示。  
  
    此用户不能浏览或查询其所属的区域之外的区域的任何 Internet 销售数据，因为在 Sales Employees by Territory 用户角色中为 Sales Territory 表定义的行筛选器有效地保护了与其他销售区域相关的所有数据。  
  
## <a name="see-also"></a>请参阅  
[USERNAME 函数 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)  
[LOOKUPVALUE 函数 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)  
[CUSTOMDATA 函数 (DAX)](http://msdn.microsoft.com/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
