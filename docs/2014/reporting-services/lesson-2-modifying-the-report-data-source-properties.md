---
title: 第 2 课：修改报表数据源属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 41746f2938afd17e59dc4a9f2278179e4ccc1695
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225124"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>第 2 课：修改报表数据源属性
  在本课中，您将使用报表管理器来选择要传递给收件人的报表。 你将定义的数据驱动订阅将分发在 **创建基本表报表（SSRS 教程）** 教程中创建的 [创建基本表报表（SSRS 教程）](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)报表。 在接下来的步骤中，将修改此报表使用的数据源连接信息，以获取数据。 只有使用 **已存储凭据** 访问报表数据源的报表才能通过数据驱动订阅进行分发。 已存储凭据是处理无人参与的报表所必需的。  
  
 您还将修改数据集和报表以便使用参数来筛选 `[Order]` 上的报表，这样，订阅可为特定的顺序和呈现格式输出不同的报表实例。  
  
 **本主题内容：**  
  
-   [若要修改的数据源属性](#bkmk_modify_datasource)  
  
-   [修改 AdventureWorksDataset](#bkmk_modify_dataset)  
  
-   [若要添加报表参数并重新发布报表](#bkmk_add_reportparameter)  
  
-   [若要重新部署报表](#bkmk_redeploy)  
  
##  <a name="bkmk_modify_datasource"></a> 若要修改的数据源属性  
  
1.  启动[报表管理器&#40;SSRS 本机模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)使用管理员权限，例如，右键单击 Internet Explorer 图标，单击**以管理员身份运行**。  
  
2.  浏览到包含 **Sales Orders** 报表的文件夹，在该报表的上下文菜单中，单击 **“管理”**。  
  
     ![打开报表上下文菜单并选择管理](../../2014/tutorials/media/ssrs-tutorial-datadriven-manage-report.gif "打开报表上下文菜单并选择管理")  
  
3.  单击 **“数据源”** 选项卡。  
  
4.  对于 **“连接类型”**，请选择 **Microsoft SQL Server**。  
  
5.  自定义数据源连接字符串如下并且它假定示例数据库位于本地数据库服务器上：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2012  
    ```  
  
6.  单击 **“安全存储在报表服务器中的凭据”**。  
  
7.  输入用户名（使用 *domain\user* 格式）和密码。 如果您没有访问 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库的权限，请指定具有此权限的登录名。  
  
8.  单击 **“在与数据源建立连接时用作 Windows 凭据”**，再单击 **“确定”**。 如果没有使用域帐户（例如，如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登录），请不要单击该复选框。  
  
9. 若要验证是否能连接到数据源，请单击 **“测试连接”** 。  
  
10. 单击 **“应用”**。  
  
11. 查看报表以验证报表是否以指定的凭据运行。 若要查看报表，请单击“查看”  选项卡。注意，报表处于打开状态后，必须选中雇员姓名，然后单击 **“查看报表”** 按钮，以查看该报表。  
  
##  <a name="bkmk_modify_dataset"></a> 修改 AdventureWorksDataset  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中打开 Sales Orders 报表。  
  
2.  右键单击数据集 `AdventureWorksDataset`，然后单击“数据集属性”。  
  
3.  将语句 `WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)` 添加到 `Group By` 语句之前。 完整查询语法如下所示：  
  
    ```  
    SELECT soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal)  AS LineTotal  
    FROM Sales.SalesPerson AS sp INNER JOIN  
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN  
       Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID INNER JOIN  
       Production.Product AS pp ON sd.ProductID = pp.ProductID  
    INNER JOIN  
       Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID   
    INNER JOIN  
        Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID  
  
    WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)  
  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID  
    HAVING (ppc.Name = 'Clothing')  
    ```  
  
4.  单击 **“确定”**。  
  
##  <a name="bkmk_add_reportparameter"></a> 若要添加报表参数并重新发布报表  
  
1.  在 **“报表数据”** 窗格中，单击 **“新建”** ，然后单击 **“参数...”**。  
  
2.  在 **“名称”** 中，键入 `OrderNumber`。  
  
3.  在 **“提示”** 中，键入 `OrderNumber`。  
  
4.  选择“允许空值("")”。  
  
5.  选择 **“允许 Null 值”**。  
  
6.  单击“确定” 。 该参数将添加到 **“报表数据窗格”** ，其外观如下图所示：  
  
     ![新参数添加到报表数据窗格](../../2014/tutorials/media/ssrs-tutorial-datadriven-parameter.gif "新参数添加到报表数据窗格")  
  
7.  单击 **“预览”** 选项卡，运行该报表。请注意报表顶部的参数输入框。 您可以：  
  
    -   在不使用参数的情况下单击“查看报表”以便看到完整的报表。  
  
    -   取消选择 Null 选项，然后键入订单号，例如 so71949，以便只查看报表中的一个订单。  
  
         ![报表查看器中的使用参数区域可见](../../2014/tutorials/media/ssrs-tutorial-datadriven-reportviewer-parameter.gif "参数区可见的报表查看器")  
  
8.  重新部署报表，以便下一课程中的订阅配置可利用您在本课程中进行的更改。 在表教程中使用的项目属性的详细信息，请参阅将报表发布到报表服务器 （可选） 一节的[第 6 课：添加分组和总计 &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)。  
  
##  <a name="bkmk_redeploy"></a> 若要重新部署报表  
  
1.  重新部署报表，以便下一课程中的订阅配置可利用您在本课程中进行的更改。 在表教程中使用的项目属性的详细信息，请参阅将报表发布到报表服务器 （可选） 一节的[第 6 课：添加分组和总计 &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)。  
  
2.  在工具栏上，单击 **“生成”** ，然后单击 **“部署教程”**。  
  
## <a name="next-steps"></a>后续步骤  
 您已成功配置了报表，从而可使用已存储凭据获取数据。 接下来，将使用报表管理器中的“数据驱动订阅”页来指定订阅。 请参阅[第 3 课：定义数据驱动订阅](../reporting-services/lesson-3-defining-a-data-driven-subscription.md)。  
  
## <a name="see-also"></a>请参阅  
 [管理报表数据源](report-data/manage-report-data-sources.md)   
 [为报表数据源指定凭据和连接信息](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [创建数据驱动订阅（SSRS 教程）](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [创建基本表报表（SSRS 教程）](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
