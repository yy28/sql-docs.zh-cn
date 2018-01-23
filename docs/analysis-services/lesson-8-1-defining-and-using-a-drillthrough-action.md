---
title: "定义和使用钻取操作 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 3765f865-2b93-44be-b290-28e3815d5ecb
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: d15da8a4d463cbe2e8b0b05abf163400dc354749
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2018
---
# <a name="lesson-8-1---defining-and-using-a-drillthrough-action"></a>课程 8-1-定义和使用钻取操作
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

如果按事实维度来维度化事实数据，而不正确筛选查询返回的数据，则可能导致查询速度变慢。 若要避免出现这种情况，可以定义对返回的总行数进行限制的钻取操作。 这将极大地提高查询性能。  
  
在本主题的任务中，将定义钻取操作，以返回通过 Internet 对客户进行销售的订单详细信息。  
  
## <a name="defining-the-drillthrough-action-properties"></a>定义钻取操作属性  
  
1.  在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器中，单击“操作”选项卡。  
  
    “操作”选项卡中包括几个窗格。 在选项卡的左侧是“操作组织程序”窗格和“计算工具”窗格。 这两个窗格的右侧是“显示”窗格，其中可以显示“操作组织程序”窗格中所选操作的详细信息。  
  
    下图显示了多维数据集设计器的“操作”选项卡。  
  
    ![多维数据集设计器操作选项卡](../analysis-services/media/l8-action1.gif "多维数据集设计器操作选项卡")  
  
2.  在“操作”选项卡的工具栏上，单击“新建钻取操作”按钮。  
  
    “显示”窗格中将出现空白操作模板。  
  
    ![在显示窗格中的空白操作模板](../analysis-services/media/l8-action2.gif "空的操作在显示窗格中的模板")  
  
3.  在“名称”框中，将此操作的名称更改为 **Internet Sales Details Drillthrough Action**。  
  
4.  在“度量值组成员”列表中，选择“Internet 销售”。  
  
5.  在“钻取列”框中，选择“维度”列表中的“Internet 销售订单详细信息”。  
  
6.  在“返回列”列表中，选中“项说明”和“订单编号”复选框，再单击“确定”。 下图显示至此在该操作过程中操作模板的应有外观。  
  
    ![钻取列框](../analysis-services/media/l8-action3.gif "钻取列中")  
  
7.  展开“附加属性”框，如下图所示。  
  
    ![其他属性框](../analysis-services/media/l8-action4.gif "其他属性框")  
  
8.  在“最大行数”框中键入 **10**。  
  
9. 在“标题”框中，键入 **Drillthrough to Order Details…**。  
  
    这些设置将限制返回的行数，并指定在客户端应用程序菜单中将出现的标题。 下图显示了“附加属性”框中的这些设置。  
  
    ![其他属性框](../analysis-services/media/l8-action5.gif "其他属性框")  
  
## <a name="using-the-drillthrough-action"></a>使用钻取操作  
  
1.  在“生成”菜单上，单击“部署 Analysis Services 教程”。  
  
2.  在部署成功完成后，在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器中单击“浏览器”选项卡，再单击“重新连接”按钮。  
  
3.  启动 Excel。  
  
4.  将“Internet 销售 - 销售额”度量值添加到“值”区域。  
  
5.  将“客户所在地域”用户定义层次结构从“客户”维度的“位置”文件夹添加到“报表筛选器”区域。  
  
6.  在数据透视表上的“客户所在地域”中，添加选择单个客户的筛选器。 依次展开“全部客户”、**Australia**、**Queensland**、**Brisbane**、**4000**，然后选中“Adam Powell”复选框，再单击“确定”。  
  
    [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 对 Adam Powell 的产品销售总额显示在数据区域中。  
  
7.  右键单击销售额，指向“其他操作”，然后单击“钻取订单详细信息”。  
  
    交付给 Adam Powell 的订单的详细信息将显示在“数据示例查看器”中，如下图所示。 但是，某些其他详细信息也会是有用的，如订单日期、截止日期和发运日期。 在下一个过程中，您将添加这些其他详细信息。  
  
    ![Adam Powell 发往订单](../analysis-services/media/l8-action6.gif "到 Adam Powell 已发货的订单")  
  
8.  关闭 Excel/  
  
## <a name="modifying-the-drillthrough-action"></a>修改钻取操作  
  
1.  打开“Internet 销售订单详细信息”维度的维度设计器。  
  
    注意，仅为此维度定义了三个属性。  
  
2.  在“数据源视图”窗格中，右键单击空白的区域，再单击“显示所有表”。  
  
3.  在“格式”菜单上，指向“自动版式”，然后单击“关系图”。  
  
4.  通过右键单击“数据源视图”窗格中的空白区域来查找 **InternetSales (dbo.FactInternetSales)** 表。 然后单击“查找表”，并单击“InternetSales”，再单击“确定”。  
  
5.  基于以下列创建新属性：  
  
    -   OrderDateKey  
  
    -   DueDateKey  
  
    -   ShipDateKey  
  
6.  将“订单日期键”特性的“名称”属性更改为“订单日期”，然后单击“名称列”属性的“浏览”按钮，并且在“名称列”对话框中，选择“日期”作为源表，并选择 SimpleDate 作为源列。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  将“截止日期键”特性的“名称”属性更改为“截止日期”，然后，将同一方法用于“订单日期键”特性，将此特性的“名称列”属性更改为 **Date.SimpleDate (WChar)**。  
  
8.  将“装运日期键”特性的“名称”属性更改为“装运日期”，然后将此特性的“名称列”属性更改为 **Date.SimpleDate (WChar)**。  
  
9. 切换到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器的“操作”选项卡。  
  
10. 在“钻取列”框中，选择各复选框以将以下列添加到“返回列”列表，再单击“确定”：  
  
    -   Order Date  
  
    -   Due Date  
  
    -   Ship Date  
  
    下图显示了这些所选列。  
  
    ![钻取列框](../analysis-services/media/l8-action7.gif "钻取列中")  
  
## <a name="reviewing-the-modified-drillthrough-action"></a>检查修改后的钻取操作  
  
1.  在“生成”菜单上，单击“部署 Analysis Services 教程”。  
  
2.  在成功完成部署后，切换到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器中的“浏览器”选项卡，然后单击“重新连接”按钮。  
  
3.  启动 Excel。  
  
4.  通过在“值”区域中使用“Internet 销售-销售额”以及在报表筛选器中使用“客户所在地域”，重新创建数据透视表。  
  
    添加一个从“所有客户”、**Australia**、**Queensland**、**Brisbane**、**4000**、**Adam Powell** 进行选择的筛选器。  
  
5.  单击“Internet 销售-销售额”数据单元，指向“其他操作”，然后单击“钻取订单详细信息”。  
  
    在临时电子表格中将显示交付给 Adam Powell 的这些订单的详细信息。 这包括项说明、订单号、订单日期、截止日期和发运日期信息，如下图所示。  
  
    ![Adam Powell 发往订单](../analysis-services/media/l8-action8.gif "到 Adam Powell 已发货的订单")  
  
## <a name="next-lesson"></a>下一课  
[Lesson 9: Defining Perspectives and Translations](../analysis-services/lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>另请参阅  
[操作（Analysis Services - 多维数据）](../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)  
[多维模型中的操作](../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
[维度关系](../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
[定义事实关系](../analysis-services/lesson-5-2-defining-a-fact-relationship.md)  
[定义事实关系和事实关系属性](../analysis-services/multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)  
  
  
  
