---
title: 定义数据源视图 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: af00938a-5a06-4fae-b2fc-f3fb0ca3cea5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca6e9661c65098bed1175c7108b18a482b14a542
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730326"
---
# <a name="defining-a-data-source-view"></a>定义数据源视图
  定义了将在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目中使用的数据源后，下一步通常是定义项目的数据源视图。 数据源视图是元数据的单个统一视图，这些元数据来自数据源在项目中定义的指定表和视图。 通过在数据源视图中存储元数据，可以在开发过程中使用元数据，而无需打开与任何基础数据源的连接。 有关详细信息，请参阅 [多维模型中的数据源视图](multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
 在以下任务中，定义一个数据源视图，其中包括来自 **AdventureWorksDW2012** 数据源的五个表。  
  
### <a name="to-define-a-new-data-source-view"></a>定义一个新的数据源视图  
  
1.  在解决方案资源管理器中（在 Microsoft Visual Studio 窗口的右侧），右键单击“数据源视图”，然后单击“新建数据源视图”。  
  
2.  在“欢迎使用数据源视图向导”页中，单击“下一步”。 此时将显示“选择数据源”页。  
  
3.  已选中“关系数据源”下的 **Adventure Works DW 2012** 数据源。 单击“下一步” 。  
  
    > [!NOTE]  
    >  若要创建一个基于多个数据源的数据源视图，必须先定义一个基于单一数据源的数据源视图。 此数据源将被称为主数据源。 随后，可以添加来自辅助数据源的表和视图。 在基于多个数据源中的相关表设计包含属性的维度时，可能需要将 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据源定义为主数据源，以使用其分布式查询引擎功能。  
  
4.  在“选择表和视图”页上，可以从选定的数据源提供的对象列表中选择表和视图。 可以筛选此列表，以帮助您选择表和视图。  
  
    > [!NOTE]  
    >  单击右上角中的最大化按钮，以便窗口占据整个屏幕。 这将更便于查看可用对象的完整列表。  
  
     在“可用对象”列表中，选择下列对象。 在按住 Ctrl 键的同时单击各个表可以选择多个表：  
  
    -   **DimCustomer (dbo)**  
  
    -   **DimDate (dbo)**  
  
    -   **DimGeography (dbo)**  
  
    -   **DimProduct (dbo)**  
  
    -   **FactInternetSales (dbo)**  
  
5.  单击“>”，将选中的表添加到“包含的对象”列表中。  
  
6.  单击 **“下一步”**。  
  
7.  在“名称”字段中，确保显示 **Adventure Works DW 2012**，然后单击“完成”。  
  
     此时，**Adventure Works DW 2012** 数据源视图将显示在解决方案资源管理器的“数据源视图”文件夹中。 数据源视图的内容还将显示在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的数据源视图设计器中。 此设计器包含以下元素：  
  
    -   “关系图”窗格，其中将以图形方式显示各个表及其相互关系。  
  
    -   “表”窗格，其中将以树的形式显示各个表及其架构元素。  
  
    -   “关系图组织程序”窗格，可在其中创建子关系图，用于查看数据源视图的子集。  
  
    -   一个特定于数据源视图设计器的工具栏。  
  
8.  若要最大化 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 开发环境，请单击“最大化”按钮。  
  
9. 若要在“关系图”窗格中以 50% 的缩放比例查看表，请单击“数据源视图设计器”工具栏上的“缩放”图标。 这将隐藏每个表的列详细信息。  
  
10. 若要隐藏解决方案资源管理器，请单击“自动隐藏”按钮，该按钮是标题栏上的图钉图标。 若要再次查看解决方案资源管理器，请将指针放在位于开发环境右侧的解决方案资源管理器选项卡上。 若要取消隐藏解决方案资源管理器，请再次单击“自动隐藏”按钮。  
  
11. 如果“属性”窗口在默认情况下没有隐藏，请单击该窗口和“解决方案资源管理器”窗口的标题栏上的“自动隐藏”。  
  
     现在，即可在“关系图”窗格中查看所有表及其相互关系了。 注意，在 FactInternetSales 表和 DimDate 表之间存在三种关系。 每个销售都具有三个与其关联的日期：订单日期、到期日期和发货日期。 若要查看某种关系的详细信息，可双击“关系图”窗格中的关系箭头。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [修改默认表名](lesson-1-4-modifying-default-table-names.md)  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的数据源视图](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
