---
title: "修改客户维度 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5b5aed99-1760-4bc7-b248-52ecb0b97ebc
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7ba21519d0ea16952d3aa4cc086fc78309a2108
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-3-2---modifying-the-customer-dimension"></a>Lesson 3-2-修改客户维度
可以使用许多不同的方式提高多维数据集中的维度的可用性和功能。 在本主题的各任务中，您将修改“客户”维度。  
  
## <a name="renaming-attributes"></a>重命名属性  
可以使用维度设计器的“维度结构”选项卡更改属性名称。  
  
#### <a name="to-rename-an-attribute"></a>重命名属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，切换到“客户”维度的“维度设计器”。 为此，请在解决方案资源管理器的“维度”节点中双击“客户”维度。  
  
2.  在“属性”窗格中，右键单击“英语国家/地区区域名”，然后单击“重命名”。 将该特性的名称更改为“国家/地区-区域”。  
  
3.  以相同方法更改以下属性的名称：  
  
    -   “英语教育”属性 - 更改为“教育”  
  
    -   “英语职业”属性 - 更改为“职业”  
  
    -   “省/自治区/直辖市名”属性 - 更改为“省/自治区/直辖市”  
  
4.  在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="creating-a-hierarchy"></a>创建层次结构  
通过将属性从“属性”窗格拖至“层次结构”窗格可以创建新的层次结构。  
  
#### <a name="to-create-a-hierarchy"></a>创建层次结构  
  
1.  将“国家/地区-区域”属性从“属性”窗格拖动到“层次结构”窗格中。  
  
2.  将“省/自治区/直辖市”属性从“属性”窗格拖动到位于“国家/地区-区域”级别下方的“层次结构”窗格的 **<new level>** 单元格中。  
  
3.  将“市县”属性从“属性”窗格拖动到位于“省/自治区/直辖市”级别下方的“层次结构”窗格的 **<new level>** 单元格中。  
  
4.  在“维度结构”选项卡的“层次结构”窗格中，右键单击“层次结构”的层次结构的标题栏，选择“重命名”，并键入“客户所在地域”。  
  
    此层次结构的名称现在为“客户所在地域”。  
  
5.  在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="adding-a-named-calculation"></a>添加命名计算  
可以向数据源视图的表中添加命名计算，命名计算是一个表示为计算列的 SQL 表达式。 该表达式的显示形式和工作方式类似于表中的列。 通过命名计算，不必修改基础数据源中的表即可扩展数据源视图中现有表的关系架构。 有关详细信息，请参阅 [在数据源视图中定义命名计算 (Analysis Services)](../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
#### <a name="to-add-a-named-calculation"></a>添加命名计算  
  
1.  在解决方案资源管理器中双击“数据源视图”文件夹中的“[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012”数据源视图，将其打开。  
  
2.  在左侧的“表”窗格中，右键单击 **Customer**，然后单击“新建命名计算”。  
  
3.  在“创建命名计算”对话框中，在“列名”框中键入 **FullName**，然后在“表达式”框中键入或复制并粘贴以下 **CASE**语句：  
  
    ```  
    CASE  
       WHEN MiddleName IS NULL THEN  
       FirstName + ' ' + LastName  
       ELSE  
       FirstName + ' ' + MiddleName + ' ' + LastName  
    END  
    ```  
  
    **CASE**语句将 **FirstName**、**MiddleName** 和 **LastName**列串联为一个列，该列将在“客户”维度中用作“客户”属性的显示名称。  
  
4.  单击“确定”，然后展开“表”窗格中的 **Customer**。  
  
    **FullName**命名计算显示在 Customer 表中列的列表中，并由一个图标指示它是命名计算。  
  
5.  在“文件”  菜单上，单击“全部保存” 。  
  
6.  在“表”窗格中，右键单击 **Customer**，然后单击“浏览数据”。  
  
7.  查看“浏览 Customer 表”视图中的最后一列。  
  
    注意，**FullName**列显示在数据源视图中，正确串联基础数据源中多个列的数据，而不修改原始数据源。  
  
8.  关闭“浏览 Customer 表”选项卡。  
  
## <a name="using-the-named-calculation-for-member-names"></a>将命名计算用于成员名称  
在数据源视图中创建命名计算后，可以将命名计算用作特性的属性。  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>将命名计算用于成员名称  
  
1.  切换到“客户”维度的维度设计器。  
  
2.  在“维度结构”选项卡的“属性”窗格中，单击“客户键”属性。  
  
3.  打开“属性”窗口并单击标题栏上的“自动隐藏”按钮，以便该窗口保持打开状态。  
  
4.  在“名称”属性字段中，键入“全名”。  
  
5.  在底部的 **NameColumn** 属性字段中单击，然后单击浏览 (**…**) 按钮以打开“名称列”对话框。  
  
6.  选择位于“源列”列表底部的 **FullName**，然后单击“确定”。  
  
7.  在“维度结构”选项卡中，将“全名”属性从“属性”窗格拖动到位于“市县”级别下方的“层次结构”窗格的 **<new level>** 单元格中。  
  
8.  在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="defining-display-folders"></a>定义显示文件夹  
可以使用显示文件夹将用户和属性层次结构分组为文件夹结构，以提高可用性。  
  
#### <a name="to-define-display-folders"></a>定义显示文件夹  
  
1.  打开“客户”维度的“维度结构”选项卡。  
  
2.  在“属性”窗格中，按住 Ctrl 键的同时单击下列各个属性，将它们选中：  
  
    -   **City**  
  
    -   **国家/地区-区域**  
  
    -   **Postal Code**  
  
    -   **省/市/自治区**  
  
3.  在“属性”窗口中，单击顶部的 **AttributeHierarchyDisplayFolder** 属性字段（你可能需要指向它才能看到完全名称），然后键入 **Location**。  
  
4.  在“层次结构”窗格中，单击“客户所在地域”，然后在右侧的“属性”窗口中选择“位置”作为 **DisplayFolder** 属性的值。  
  
5.  在“属性”窗格中，按住 Ctrl 键的同时单击下列各个属性，将它们选中：  
  
    -   **上下班路程**  
  
    -   **教育**  
  
    -   **性别**  
  
    -   **House Owner Flag**  
  
    -   **婚姻状况**  
  
    -   **Number Cars Owned**  
  
    -   **Number Children At Home**  
  
    -   **职业**  
  
    -   **Total Children**  
  
    -   **Yearly Income**  
  
6.  在“属性”窗口中，单击顶部的 **AttributeHierarchyDisplayFolder** 属性字段并键入 **Demographic**。  
  
7.  在“属性”窗格中，按住 Ctrl 键的同时单击下列各个属性，将它们选中：  
  
    -   **Email Address**  
  
    -   **Phone**  
  
8.  在“属性”窗口中，单击 **AttributeHierarchyDisplayFolder** 属性字段，并键入“联系人”。  
  
9. 在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="defining-composite-keycolumns"></a>定义组合的 KeyColumns  
**KeyColumns** 属性中包含表示特性键的一个或多个列。 在本课中，你会为“市县”和“	省/自治区/直辖市”属性创建组合键。 需要唯一标识属性时，组合键可能会有帮助。 例如，在本教程的稍后部分定义属性关系时，“市县”属性必须唯一确定“省/市/自治区”属性。 但是，在不同的省/自治区可能有些城市会重名。 为此，将创建由“市县”属性的 **StateProvinceName** 和 **City**列组成的组合键。 有关详细信息，请参阅[修改特性的 KeyColumn 属性](../analysis-services/multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)。  
  
#### <a name="to-define-composite-keycolumns-for-the-city-attribute"></a>若要为“市县”属性定义组合的 KeyColumns  
  
1.  打开“客户”维度的“维度结构”选项卡。  
  
2.  在“属性”窗格中，单击“市县”属性。  
  
3.  在“属性”窗口中，在靠近底部的 **KeyColumns** 字段中单击，然后单击浏览 (**...**) 按钮。  
  
4.  在“键列”对话框的“可用列”列表中，选择 **StateProvinceName** 列，然后单击 **>** 按钮。  
  
    现在，**City** 和 **StateProvinceName** 列会显示在“键列”列表中。  
  
5.  单击 **“确定”**。  
  
6.  若要设置“市县”特性的 **NameColumn** 属性，请在“属性”窗口的 **NameColumn** 字段中单击，然后单击浏览 (**...**) 按钮。  
  
7.  在“名称列” 对话框的“源列”列表中，选择 **City**，然后单击“确定”。  
  
8.  在“文件”  菜单上，单击“全部保存” 。  
  
#### <a name="to-define-composite-keycolumns-for-the-state-province-attribute"></a>为“省/市/自治区”属性定义组合的 KeyColumns  
  
1.  确保“客户”维度的“维度结构”选项卡处于打开状态。  
  
2.  在“属性”窗格中，单击“省/自治区/直辖市”属性。  
  
3.  在“属性”窗口中，在 **KeyColumns** 字段中单击，然后单击浏览 (**...**) 按钮。  
  
4.  在“键列”对话框的“可用列”列表中，选择 **EnglishCountryRegionName** 列，然后单击 **>** 按钮。  
  
    现在，**EnglishCountryRegionName** 和 **StateProvinceName** 列会显示在“键列”列表中。  
  
5.  单击 **“确定”**。  
  
6.  若要设置“省/自治区/直辖市”特性的 **NameColumn** 属性，请在“属性”窗口的 **NameColumn** 字段中单击，然后单击浏览 (**...**) 按钮。  
  
7.  在“名称列”对话框的“源列”列表中，选择 **StateProvinceName**，然后单击“确定”。  
  
8.  在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="defining-attribute-relationships"></a>定义属性关系  
如果基础数据支持，则应定义属性间的属性关系。 定义属性关系可加快维度、分区和查询处理的速度。 有关详细信息，请参阅 [定义属性关系](../analysis-services/multidimensional-models/attribute-relationships-define.md) 和 [属性关系](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
#### <a name="to-define-attribute-relationships"></a>定义属性关系  
  
1.  在“客户”维度的“维度设计器”中，单击“属性关系”选项卡。您可能需要等待。  
  
2.  在关系图中，右键单击“市县”属性，然后单击“新建属性关系”。  
  
3.  在“创建属性关系”对话框中，“源属性”是“市县”。 将“相关属性”设置为“省/市/自治区”。  
  
4.  在“关系类型”列表中，将关系类型设置为“刚性”。  
  
    因为各成员之间的关系不会随时间变化，所以此关系类型为“刚性”。 例如，某个市县不太可能成为另一个省/市/自治区的一部分。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  在关系图中，右键单击“省/市/自治区”属性，然后选择“新建属性关系”。  
  
7.  在“创建属性关系”对话框中，“源属性”是“省/市/自治区”。 将“相关属性”设置为“国家/地区-区域”。  
  
8.  在“关系类型”列表中，将关系类型设置为“刚性”。  
  
9. 单击 **“确定”**。  
  
10. 在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="deploying-changes-processing-the-objects-and-viewing-the-changes"></a>部署更改、处理对象以及查看更改  
更改属性和层次结构后，必须部署更改并重新处理相关对象，然后才能查看这些更改。  
  
#### <a name="to-deploy-the-changes-process-the-objects-and-view-the-changes"></a>部署更改、处理对象以及查看更改  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的“生成”菜单中，单击“部署 Analysis Services 教程”。  
  
2.  在收到“部署成功完成”消息后，单击“客户”维度的维度设计器的“浏览器”选项卡，然后单击设计器工具栏左侧的“重新连接”按钮。  
  
3.  确保在“层次结构”列表中选择了“客户所在地域”，然后在浏览器窗格中依次展开“全部”、**Australia**、**New South Wales**和 **Coffs Harbour**。  
  
    浏览器会将客户显示在市县中。  
  
4.  切换到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的“多维数据集设计器”。 为此，请在“解决方案资源管理器”的“多维数据集”节点中，双击“Analysis Services 教程”多维数据集。  
  
5.  单击“浏览器”选项卡，然后在设计器的工具栏上单击“重新连接”按钮。  
  
6.  在“度量值组”窗格中，展开“客户”。  
  
    注意，“客户”下只出现没有显示文件夹值的显示文件夹和属性，而不显示属性的较长列表。  
  
7.  在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[修改“产品”维度](../analysis-services/lesson-3-3-modifying-the-product-dimension.md)  
  
## <a name="see-also"></a>另请参阅  
[维度特性属性参考](../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
[从维度中删除属性](../analysis-services/multidimensional-models/attribute-properties-remove-an-attribute-from-a-dimension.md)  
[重命名属性](../analysis-services/multidimensional-models/attribute-properties-rename-an-attribute.md)  
[在数据源视图中定义命名计算 (Analysis Services)](../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  

