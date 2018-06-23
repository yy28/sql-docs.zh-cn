---
title: 通过使用行筛选器实现动态安全性 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8bf03c45-caf5-4eda-9314-e4f8f24a159f
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: 066e628cc40f4ac4745f4b2edaa93ecdbd8d93d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137440"
---
# <a name="implement-dynamic-security-by-using-row-filters"></a>通过使用行筛选器实现动态安全性
  在本补充课程中，您将另外创建一个实现动态安全性的角色。 动态安全性提供了基于当前登录用户的用户名或登录 ID 的行级别安全性。 若要了解详细信息，请参阅[角色（SSAS 表格）](../analysis-services/tabular-models/roles-ssas-tabular.md)。  
  
 若要实现动态安全性，您必须向模型中添加一个表，该表中包含那些可以创建与模型的连接作为数据源并可浏览模型对象和数据的用户的 Windows 用户名。 您使用本教程创建的模型位于 Adventure Works Corp. 上下文中；但是，若要完成本课程，您必须添加一个表，其中包含来自您自己域的用户。 您不需要将添加的用户名的密码。 若要使用您自己域中的少量示例用户创建一个 Employee Security 表，您需要使用粘贴功能，从 Excel 电子表格中粘贴员工数据。 在实际应用场景中，包含添加到模型中的用户名的表通常将使用实际数据库中的表作为数据源；例如，实际的 dimEmployee 表。  
  
 若要实现动态安全性，你将使用两个新的 DAX 函数：[用户名函数&#40;DAX&#41; ](https://msdn.microsoft.com/library/hh230954.aspx)和[LOOKUPVALUE 函数&#40;DAX&#41;](https://msdn.microsoft.com/library/gg492170.aspx)。 这两个函数在新角色中进行定义，应用在行筛选器公式中。 该公式使用 LOOKUPVALUE 函数从 Employee Security 表指定一个值，然后将该值传递给 USERNAME 函数，后者指定登录用户的用户名属于此角色。 之后，该用户只能浏览此角色的行筛选器指定的数据。 在这种情况下，您将指定销售员工只能浏览自己为其中成员的销售区域的 Internet 销售数据。  
  
 若要完成本补充课程，您将需要完成一系列任务。 这些任务是此 Adventure Works 表格模型方案所特有的，但并不一定适用于实际的应用场景。 每个任务都包含描述任务目的的附加信息。  
  
 学完本课的估计时间： **30 分钟**  
  
## <a name="prerequisites"></a>必要條件  
 本补充课程主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本补充课程中的任务之前，您应已完成所有之前的课程。  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>将 dimSalesTerritory 表添加到 AW Internet Sales 表格模型项目中  
 若要为此 Adventure Works 方案实现动态安全性，您必须向模型中另外添加两个表。 第一个要添加的表是来自同一 AdventureWorksDW 数据库的 dimSalesTerritory（作为 Sales Territory）。 稍后，您将会对 Sales Territory 表应用行筛选器，以定义登录用户可以浏览的特定数据。  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>添加 dimSalesTerritory 表  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“现有连接”**。  
  
2.  在“现有连接”对话框中，确认已选中“Adventure Works DB from SQL”数据源连接，然后单击“打开”。  
  
     如果出现“模拟凭据”对话框，请键入您在“第 2 课：添加数据”中使用的模拟凭据。  
  
3.  在“选择如何导入数据”页上，保持选中“从表和视图的列表中进行选择，以便选择要导入的数据”，然后单击“下一步”。  
  
4.  在“选择表和视图”页上，选择“DimSalesTerritory”表。  
  
5.  在“友好名称”列中，键入 **Sales Territory**。  
  
6.  单击“预览并筛选”。  
  
7.  取消选择“SalesTerritoryAlternateKey”列，然后单击“确定”。  
  
8.  在“选择表和视图”页上，单击“完成”。  
  
     新表将添加到模型工作区中。 源 dimSalesTerritory 表中的对象和数据随后将导入到 AW Internet Sales 表格模型中的新 Sales Territory 表中。  
  
9. 导入该表后，单击“关闭”。  
  
## <a name="give-the-columns-friendly-names"></a>为列指定友好名称  
 在此任务中，您将重命名 Sales Territory 表中的列，为它们指定友好名称。 并不总是要为表和/或列指定友好名称；不过这样做以后，更易于在模型设计器中导航您的模型项目，用户也更易于浏览客户端应用程序字段列表中的模型对象和数据。  
  
#### <a name="to-rename-columns-in-the-sales-territory-table"></a>重命名 Sales Territory 表中的列  
  
-   在模型设计器中，重命名“Sales Territory”表中的列：  
  
     **销售区域**  
  
    |源名称|友好名称|  
    |-----------------|-------------------|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesTerritoryRegion|销售区域所属地区|  
    |SalesTerritoryCountry|销售区域所属国家/地区|  
    |SalesTerritoryGroup|销售区域组|  
  
## <a name="add-a-table-with-user-name-data"></a>向表中添加用户名数据  
 由于 AdventureWorksDW 示例数据库中的 dimEmployee 表包含来自 AdventureWorks 域的用户，而您自己的环境中不存在这些用户名，因此必须在您的模型中创建一个表，包含您组织中的少量实际示例用户（三个用户）。 然后，将这些用户作为成员添加到新角色中。 您不需要示例用户名的密码，但需要来自您自己域的实际 Windows 用户名。  
  
#### <a name="to-add-an-employee-security-table"></a>添加 Employee Security 表  
  
1.  打开 Microsoft Excel，创建一个新工作表。  
  
2.  复制下面的表（包括标题行），然后将其粘贴到该工作表中。  
  
    |Employee Id|Sales Territory Id|First Name|Last Name|Login Id|  
    |-----------------|------------------------|----------------|---------------|--------------|  
    |@shouldalert|2|\<第一个用户名 >|\<最后一个用户名 >|\<域 \ 用户名 >|  
    |@shouldalert|3|\<第一个用户名 >|\<最后一个用户名 >|\<域 \ 用户名 >|  
    |2|4|\<第一个用户名 >|\<最后一个用户名 >|\<域 \ 用户名 >|  
    |3|5|\<第一个用户名 >|\<最后一个用户名 >|\<域 \ 用户名 >|  
  
3.  在新工作表中，将 first name、last name 和 domain\username 替换为您组织中的三个用户的姓名和登录 ID。 将同一个用户置于前两行，Employee Id 为 1。 这表示此用户属于多个销售区域。 保持 Employee Id 和 Sales Territory Id 字段不变。  
  
4.  保存该工作表作为`Sample Employee`。  
  
5.  在该工作表中，选择包含员工数据的所有单元（包括标题），在所选数据上右键单击，然后单击“复制”。  
  
6.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“编辑”菜单，然后单击“粘贴”。  
  
     如果“粘贴”灰显，请单击模型设计器窗口中的任意表中的任意列，然后依次单击“编辑”菜单和“粘贴”。  
  
7.  在**粘贴预览**对话框中，在**表名**，类型`Employee Security`。  
  
8.  在“要粘贴的数据”中，确认数据包含“Sample Employee”工作表中的所有用户数据和标题。  
  
9. 确认已选中“使用第一行作为列标题”，然后单击“确定”。  
  
     包含从 Sample Employee 工作表复制的员工数据的名为“Employee Security”的新表即已创建。  
  
## <a name="create-relationships-between-internet-sales-geography-and-sales-territory-table"></a>在“Internet Sales”、“Geography”和“Sales Territory”表之间创建关系  
 Internet Sales、Geography 和 Sales Territory 表全部包含共同列 Sales Territory Id。Sales Territory 表中的 Sales Territory Id 列包含每个销售区域不同 ID 的值。  
  
#### <a name="to-create-relationships-between-the-internet-sales-geography-and-the-sales-territory-table"></a>在 Internet Sales、Geography 和 Sales Territory 表之间创建关系  
  
1.  在模型设计器的“关系图视图”中，在“Geography”表中单击并按住“Sales Territory Id”列，将光标拖到“Sales Territory”表中的“Sales Territory Id”列，然后释放。  
  
2.  在“Internet Sales”表中单击并按住“Sales Territory Id”列，将光标拖到“Sales Territory”表中的“Sales Territory Id”列，然后释放。  
  
     注意，此关系的 Active 属性为 False，表示它不活动。 这是因为 Internet Sales 表已有另一个在度量值中使用的活动关系。  
  
## <a name="hide-the-employee-security-table-from-client-applications"></a>在客户端应用程序中隐藏 Employee Security 表  
 在此任务中，您将隐藏 Employee Security 表，使其不显示在客户端应用程序的字段列表中。 请记住，隐藏表并不会保护表安全。 用户仍可以查询 Employee Security 表数据，如果他们知道怎么查询的话。 若要保护 Employee Security 表数据的安全，以阻止用户能够查询其任何数据，您将需要在后面的任务中应用筛选器。  
  
#### <a name="to-hide-the-employee-table-from-client-applications"></a>在客户端应用程序中隐藏 Employee 表  
  
-   在模型设计器的“关系图视图”中，右键单击“Employee”表标题，然后单击“从客户端工具中隐藏”。  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>创建 Sales Employees by Territory 用户角色  
 在此任务中，您将创建一个新的用户角色。 此角色将包含一个行筛选器，用于定义 Sales Territory 表的哪些行对用户可见。 然后，此筛选器将在一对多关系方向中应用于与 Sales Territory 相关的所有其他表。 您还将应用一个简单的筛选器，使属于此角色成员的所有用户都无法查询整个 Employee Security 表。  
  
> [!NOTE]  
>  您在本课程中创建的 Sales Employees by Territory 角色将限制成员只浏览（或查询）其所属的销售区域的销售数据。 如果将某一用户添加为 Sales Employees by Territory 角色的成员，而该用户也同时作为在[第 12 课：创建角色](../analysis-services/lesson-11-create-roles.md)中创建的角色的成员，则将获得权限组合。 在某一用户是多个角色的成员时，为每个角色定义的权限和行筛选器将累积。 也就是说，该用户将具有角色组合所确定的更大权限。  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>创建 Sales Employees by Territory 用户角色  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“模型”菜单，然后单击“角色”。  
  
2.  在 **“角色管理器”** 对话框中，单击 **“新建”**。  
  
     一个具有“无”权限的新角色将添加到列表中。  
  
3.  单击该新角色，然后在**名称**列中，重命名该角色向`Sales Employees by Territory`。  
  
4.  在“权限”列中，单击下拉列表，然后选择“读取”权限。  
  
5.  单击“成员”选项卡，然后单击“添加”。  
  
6.  在“选择用户或组”对话框的“输入要选择的对象名称”中，键入在创建“Employee Security”表时使用的第一个示例用户名。 单击“检查名称”以确认该用户名有效，然后单击“确定”。  
  
     重复此步骤，添加您在创建 Employee Security 表时使用的其他示例用户名。  
  
7.  单击“行筛选器”选项卡。  
  
8.  有关`Employee Security`表中， **DAX 筛选器**列中，键入以下公式。  
  
     `=FALSE()`  
  
     在您完成公式的建立后，按 Enter。  
  
     此公式指定所有列均解析为 False 布尔条件；因此，Sales Employees by Territory 用户角色的成员不能查询 Employee Security 表的任何列。  
  
9. 对于“Sales Territory”表，键入以下公式。  
  
     `='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 'Employee Security'[Login Id], USERNAME(), 'Employee Security'[Sales Territory Id], 'Sales Territory'[Sales Territory Id])`  
  
     在您完成公式的建立后，按 Enter。  
  
     在此公式中，LOOKUPVALUE 函数返回 Employee Security[Sales Territory Id] 列的所有值，其中 Employee Security[Login Id] 与当前登录的 Windows 用户名相同，Employee Security[Sales Territory Id] 与 Sales Territory[Sales Territory Id] 相同。  
  
     然后，使用 LOOKUPVALUE 返回的 Sales Territory ID 集来限制在 Sales Territory 表中显示的行。 仅显示行的 Sales Territory ID 位于 LOOKUPVALUE 函数返回的 ID 集中的行。  
  
10. 在“角色管理器”对话框中，单击“确定”。  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>测试 Sales Employees by Territory 用户角色  
 在此任务中，您将使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的“在 Excel 中分析”功能来测试 Sales Employees by Territory 用户角色的效用。 您将指定已添加到 Employee Security 表且作为此角色的成员的用户名之一。 然后，此用户名将用作在 Excel 和模型之间创建的连接中的有效用户名。  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>测试 Sales Employees by Territory 用户角色  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“在 Excel 中分析”**。  
  
2.  在“在 Excel 中分析”对话框的“指定用于连接到模型的用户名或角色”中，选择“其他 Windows 用户”，然后单击“浏览”。  
  
3.  在“选择用户或组”对话框的“输入要选择的对象名称”中，键入包括在“Employee”表中的其中一个用户名，然后单击“检查名称”。  
  
4.  单击“确定”关闭“选择用户或组”对话框，然后单击“确定”关闭“在 Excel 中分析”对话框。  
  
     Excel 将打开，并显示一个新工作簿。 将自动创建一个数据透视表。 数据透视表字段列表包含您的新模型中提供的大多数数据字段。  
  
     请注意，Employee Security 表在数据透视表字段列表中不可见。 这是因为您在前一任务中选择了从客户端工具隐藏此表。  
  
5.  在“数据透视表字段”列表中，在“∑ Internet Sales”（度量值）中选择“Internet Total Sales”度量值。 该度量值将会输入到“值”字段中。  
  
6.  在“数据透视表字段”列表中，从“Sales Territory”表中选择“Sales Territory Id”列。 该列将会输入到“行标签”字段中。  
  
     请注意，仅显示您使用的有效用户名所属的一个区域的 Internet 销售数字。 如果您选择了另一列，例如，从 Geography 表选择 City 列作为“行标签”字段，则仅显示有效用户所属的销售区域中的城市。  
  
     此用户不能浏览或查询其所属的区域之外的区域的任何 Internet 销售数据，因为在 Sales Employees by Territory 用户角色中为 Sales Territory 表定义的行筛选器有效地保护了与其他销售区域相关的所有数据。  
  
## <a name="see-also"></a>请参阅  
 [USERNAME 函数&#40;DAX&#41;](https://msdn.microsoft.com/library/hh230954.aspx)   
 [LOOKUPVALUE 函数&#40;DAX&#41;](https://msdn.microsoft.com/library/gg492170.aspx)   
 [CUSTOMDATA 函数&#40;DAX&#41;](https://msdn.microsoft.com/library/hh213140.aspx)  
  
  