---
title: "第 2 课： 修改报表数据源属性 |Microsoft 文档"
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
caps.latest.revision: 43
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be153d2ba1469034cad5e31e5e823d6ac5be4b4e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>Lesson 2: Modifying the Report Data Source Properties
在此 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 教程课程中，你会使用 Web 门户来选择要传递给收件人的报表。 你将定义的数据驱动订阅将分发在 **创建基本表报表（SSRS 教程）** 教程中创建的 [创建基本表报表（SSRS 教程）](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)报表。  在接下来的步骤中，将修改此报表使用的数据源连接信息，以获取数据。 只有使用 **已存储凭据** 访问报表数据源的报表才能通过数据驱动订阅进行分发。 已存储凭据是处理无人参与的报表所必需的。  
  
您还将修改数据集和报表以便使用参数来筛选 `[Order]` 上的报表，这样，订阅可为特定的顺序和呈现格式输出不同的报表实例。  
  
## <a name="bkmk_modify_datasource"></a>修改数据源以使用存储的凭据  
  
1.  使用管理员权限浏览到 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] Web 门户，例如，右键单击 Internet Explorer 图标，然后单击“以管理员身份运行”。  
 
2.    浏览到 Web 门户 URL。  例如：   
    `http://<server name>/reports`中创建已分区表或索引。  
    `http://localhost/reports`
 **注意：** web*门户*URL 为"Reports"，不报告*服务器*"Reportserver"的 URL。  
3.  浏览到包含 **Sales Orders** 报表的文件夹，在该报表的上下文菜单中，单击 **“管理”**。  
 
 ![ssrs_tutorial_datadriven_manage_report](../reporting-services/media/ssrs-tutorial-datadriven-manage-report.png)
  
3.  单击**数据源**的左窗格中。  
  
4.  验证**连接类型**是**Microsoft SQL Server**。  
  
5.  验证是否连接字符串如下所示并且它假定示例数据库位于本地数据库服务器上：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
6.  单击**使用下面的凭据**。  
  
7. 在**的凭据类型**，选择**Windows 用户名和密码**
8. 键入你的用户名 (使用格式*域 \ 用户*) 和密码。 如果你没有访问 AdventureWorks2014 数据库的权限，请指定具有此权限的登录名。  
    
9. 若要验证是否能连接到数据源，请单击 **“测试连接”** 。  
  
10. 单击 **“保存”**。
11. 单击**取消**  
  
11. 查看报表以验证报表是否以指定的凭据运行。 报表。  
  
## <a name="bkmk_modify_dataset"></a>修改 AdventureWorksDataset  
 在以下步骤中，你将修改数据集以使用参数基于订单号筛选数据集。
1.  打开 **Sales Orders** 报表 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]  
  
2.  右键单击数据集 `AdventureWorksDataset`，然后单击“数据集属性”。  
    ![ssrs_tutorial_datadriven_datasetproperties](../reporting-services/media/ssrs-tutorial-datadriven-datasetproperties.png)  
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
 在以下步骤中，你将向报表添加一个参数。  该报表参数会馈送数据集参数。 
## <a name="bkmk_add_reportparameter"></a>添加报表参数并重新发布报表  
  
1.  在“报表数据”窗格中，展开参数文件夹，然后双击“Ordernumber”参数。  它在上一步中向数据集添加参数时自动创建。 单击“新建”，然后单击“参数...”  
 ![ssrs_tutorial_datadriven_parameter](../reporting-services/media/ssrs-tutorial-datadriven-parameter.png) 
2.  验证“名称”是否为 `OrderNumber`。  
  
3.  验证**提示**是`OrderNumber`。  
  
4.  选择**允许空白值 ("")**。  
  
5.  选择 **“允许 Null 值”**。  
  
6.  单击 **“确定”**。  
  
7.  单击**预览**选项卡以运行报表。 请注意报表顶部的参数输入框。 您可以：  
  
    -   在不使用参数的情况下单击“查看报表”以便看到完整的报表。  
  
    -   取消选择“Null”选项并输入订单号，例如 so71949，然后单击“查看报表”以便只在报表中查看这一个订单。  
    ![ssrs_tutorial_datadriven_reportviewer_parameter](../reporting-services/media/ssrs-tutorial-datadriven-reportviewer-parameter.png) 
 
  
## <a name="bkmk_redeploy"></a>重新部署报表  
  
1.  重新部署报表，以便下一课程中的订阅配置可利用您在本课程中进行的更改。 有关表教程中使用的项目属性的详细信息，请参阅将报表发布到报表服务器 （可选） 一节的[6 课： 添加分组和总计 &#40;Reporting Services &#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).  
  
2.  在工具栏上，单击 **“生成”** ，然后单击 **“部署教程”**。  
  
## <a name="next-steps"></a>后续步骤  
+ 你已成功地将报表配置为使用已存储凭据获取数据，并且可以使用参数筛选数据。 
+ 在下一课中，你会使用 Web 门户“数据驱动订阅”页来配置订阅。 请参阅 [第 3 课：定义数据驱动订阅](../reporting-services/lesson-3-defining-a-data-driven-subscription.md)。  
  
## <a name="see-also"></a>另请参阅  
[管理报表数据源](../reporting-services/report-data/manage-report-data-sources.md)  
[为报表数据源指定凭据和连接信息](../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
[创建数据驱动订阅（SSRS 教程）](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[创建基本表报表（SSRS 教程）](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
  


