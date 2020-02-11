---
title: 从数据馈送导入（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0686e519-67c2-4f9b-8cd2-84a4871499ee
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bcb3a1cbcabc66492bbd780be4716ce69f15de37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66080573"
---
# <a name="import-from-a-data-feed-ssas-tabular"></a>从数据馈送导入（SSAS 表格）
  数据馈送是从联机数据源生成的流向目标文档或应用程序的一个或多个 XML 数据流。 可以通过使用“表导入向导”将数据从数据馈送导入模型中。  
  
 本主题包含以下各节：  
  
-   [了解从数据馈送导入](#prereq)  
  
-   [从 Azure DataMarket 数据集导入数据](#azure)  
  
-   [从公共数据源或公司数据源导入数据馈送](#importdata)  
  
-   [从 SharePoint 列表导入数据馈送](#importlist)  
  
-   [从 Reporting Services 报表导入数据馈送](#importreport)  
  
##  <a name="prereq"></a>了解从数据馈送导入  
 可以从以下数据馈送类型中将数据导入“表格模型”：  
  
 **Reporting Services 报表**  
 可以使用已发布到 Sharepoint 站点或报表服务器的 Reporting Services 报表作为模型中的数据源。 从 Reporting Services 报表导入数据时，您必须指定报表定义 (.rdl) 文件作为数据源。  
  
 **Azure DataMarket 数据集**  
 Azure DataMarket 是一种提供单一市场和信息传递通道作为云服务的服务。 Azure DataMarket 数据集要求一个帐户键，而不是 Windows 用户帐户。  
  
 **Atom 馈送**  
 馈送必须是 Atom 馈送。 不支持 RSS 馈送。 该馈送必须可供公开使用，或您必须有权基于您当前登录所用的 Windows 帐户连接到该馈送。  
  
 在导入过程中只可一次将数据馈送中的数据添加到模型中。 若要从馈送获取更新的数据，您可以从模型设计器刷新数据，或在将数据部署到 Analysis Services 生产实例后为模型配置数据刷新计划。 有关详细信息，请参阅 [处理数据（SSAS 表格）](process-data-ssas-tabular.md)。  
  
##  <a name="azure"></a>从 Azure DataMarket 数据集导入数据  
 在模型中，可以将 Azure DataMarket 中的数据以表的形式导入。  
  
#### <a name="to-import-data-from-an-azure-datamarket-dataset"></a>从 Azure DataMarket 数据集中导入数据  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，单击 **“模型”** 菜单，然后单击 **“从数据源导入”**。 将打开“表导入向导”。  
  
2.  在 **“连接数据源”** 页的 **“数据馈送”** 下，选择 **“Azure DataMarket 数据集”**，然后单击 **“下一步”**。  
  
3.  在 **“连接到 DataMarket 数据集”** 页的 **“友好名称”** 中，为您要访问的馈送键入描述性名称。 如果您正在导入多个馈送或数据源，则将描述性名称用于连接可帮助您记住连接的使用方式。  
  
4.  在 **“数据馈送 URL”** 中，键入数据馈送的地址。  
  
5.  在 **“安全设置”** 的 **“帐户键”** 中，键入帐户键。 Analysis Services 使用帐户键来访问 DataMarket 订阅。  
  
6.  单击 **“测试连接”** 确保馈送可用。 或者，还可以单击 **“高级”** 以便确认基本 URL 或服务文档 URL 包含提供馈送的查询或服务文档。  
  
7.  单击 **“下一步”** 继续导入。  
  
8.  在 **“模拟信息”** 页中，指定刷新数据时 Analysis Services 将用于连接到数据源的凭据，然后单击 **“下一步”**。 这些凭据不同于帐户键。  
  
9. 在向导的 **“选择表和视图”** 页的 **“友好名称”** 字段中，键入标识在导入数据后将包含这些数据的表的描述性名称。  
  
10. 单击 **“预览并筛选”** 检查数据并更改列选择。 您不能限制在报表数据馈送中导入的行，但可以通过清除相应的复选框来删除列。 单击“确定”。   
  
11. 在 **“选择表和视图”** 页上，单击 **“完成”**。  
  
##  <a name="importdata"></a>从公共数据源或公司数据源导入数据馈送  
 您可以访问公共馈送，也可以生成自定义数据服务，这些服务从专有或早期数据库系统生成 Atom 馈送。  
  
#### <a name="to-import-data-from-public-or-corporate-data-feeds"></a>从公共数据馈送或公司数据馈送导入数据  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，单击 **“模型”** 菜单，然后单击 **“从数据源导入”**。 将打开“表导入向导”。  
  
2.  在 **“连接数据源”** 页的 **“数据馈送”** 下，选择 **“其他馈送”**，然后单击 **“下一步”**。  
  
3.  在 **“连接到数据馈送”** 页中，为您要访问的馈送键入描述性名称。 如果您正在导入多个馈送或数据源，则将描述性名称用于连接可帮助您记住连接的使用方式。  
  
4.  在 **“数据馈送 URL”** 中，键入数据馈送的地址。 有效值包括以下值：  
  
    1.  包含 Atom 数据的 XML 文档。 例如，下面的 URL 指向 Open Government Data Initiative 网站上的公共馈送：  
  
        ```  
        http://ogdi.cloudapp.net/v1/dc/banklocations/  
        ```  
  
    2.  指定一个或多个馈送的 .atomsvc 文档。 .atomsvc 文档指向提供一个或多个馈送的服务或应用程序。 每个馈送都指定为返回结果集的基础查询。  
  
         您可以指定一个 URL 地址，该地址指向 Web 服务器上的 .atomsvc 文档；也可以从您的计算机上的共享文件夹或本地文件夹打开文件。 如果您在导出 Reporting Services 报表时将某一 .atomsvc 文档保存到您的计算机，则可能具有 .atomsvc 文档；或者，您可能在某人为您的 SharePoint 站点创建的数据馈送库中具有 .atomsvc 文档。  
  
        > [!NOTE]  
        >  建议您指定可通过某一 URL 地址或共享文件夹访问的 .atomsvc 文档，因为这样做以后，您可以在工作簿发布到 SharePoint 后在以后为该工作簿配置自动数据刷新。 如果您指定不位于您的本地计算机上的位置，则服务器可以重复使用相同的 URL 地址或网络文件夹来刷新数据。  
  
5.  单击 **“测试连接”** 确保馈送可用。 或者，还可以单击 **“高级”** 以便确认基本 URL 或服务文档 URL 包含提供馈送的查询或服务文档。  
  
6.  单击 **“下一步”** 继续导入。  
  
7.  在 **“模拟信息”** 页中，指定刷新数据时 Analysis Services 将用于连接到数据源的凭据，然后单击 **“下一步”**。  
  
8.  在向导的 **“选择表和视图”** 页的 **“友好名称”** 字段中，使用标识在导入数据后将包含这些数据的表的描述性名称替换“数据馈送内容”。  
  
9. 单击 **“预览并筛选”** 检查数据并更改列选择。 您不能限制在报表数据馈送中导入的行，但可以通过清除相应的复选框来删除列。 单击“确定”。   
  
10. 在 **“选择表和视图”** 页上，单击 **“完成”**。  
  
##  <a name="importlist"></a>从 SharePoint 列表导入数据馈送  
 可以导入在 (SharePoint) 功能区上具有“作为数据馈送导出”**** 按钮的任何 SharePoint 列表。 可以单击此按钮将列表作为馈送导出。  
  
#### <a name="to-import-data-feeds-from-a-sharepoint-list"></a>从 SharePoint 列表导入数据馈送  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，单击 **“模型”** 菜单，然后单击 **“从数据源导入”**。  
  
2.  在 **“连接数据源”** 页的 **“数据馈送”** 下，选择 **“其他数据馈送”**，然后单击 **“下一步”**。  
  
3.  在 **“连接到数据馈送”** 页中，为您要访问的馈送键入描述性名称。 如果您正在导入多个馈送或数据源，则将描述性名称用于连接可帮助您记住连接的使用方式。  
  
4.  在 "数据馈送 URL" 中，键入列表数据服务的地址， \<并将服务器名称> 替换为您的 SharePoint 服务器的实际名称：  
  
    ```  
    http://<server-name>/_vti_bin/listdata.svc  
    ```  
  
5.  单击 **“测试连接”** 确保馈送可用。 或者，还可以单击 **“高级”** 以便确认服务文档 URL 包含列表数据服务的地址。  
  
6.  单击 **“下一步”** 继续导入。  
  
7.  在 **“模拟信息”** 页中，指定刷新数据时 Analysis Services 将用于连接到数据源的凭据，然后单击 **“下一步”**。  
  
8.  在向导的 **“选择表和视图”** 页中，选择要导入的列表。  
  
    > [!NOTE]  
    >  只能导入包含列的列表。  
  
9. 单击 **“预览并筛选”** 检查数据并更改列选择。 您不能限制在报表数据馈送中导入的行，但可以通过清除相应的复选框来删除列。 单击“确定”。   
  
10. 在 **“选择表和视图”** 页上，单击 **“完成”**。  
  
##  <a name="importreport"></a>从 Reporting Services 报表导入数据馈送  
 如果已部署 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Reporting Services，则可以使用 Atom 呈现扩展插件从现有报表生成数据馈送。  
  
#### <a name="to-import-report-data-from-a-published-reporting-services-report"></a>从已发布的 Reporting Services 报表导入报表数据  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，单击 **“模型”** 菜单，然后单击 **“从数据源导入”**。  
  
2.  在 **“连接数据源”** 页的 **“数据馈送”** 下，选择 **“报表”**，然后单击 **“下一步”**。  
  
3.  在“连接到 Microsoft SQL Server Reporting Services 报表”页的“友好的连接名称”中，键入您要访问的馈送的说明性名称。 如果您正在导入多个数据源，则为连接使用描述性名称可帮助您记住连接的使用方式。  
  
4.  单击 **“浏览”** 并选择一个报表服务器。  
  
     如果定期使用报表服务器上的报表，该服务器可能在 **“最近使用的站点和服务器”** 中列出。 否则，在“名称”中键入报表服务器的地址，然后单击 **“打开”** 以浏览报表服务器站点上的文件夹。 Report Server 的示例地址可能是 http://\<computername>/reportserver。  
  
5.  选择报表，然后单击 **“打开”**。 或者，可以在 **“名称”** 文本框中粘贴指向报表的链接，包括完整路径和报表名称。 “表导入向导”将连接到该报表，然后在预览区域中呈现它。  
  
     如果报表使用参数，则必须指定参数，否则无法创建报表连接。 执行此操作时，只有与该参数值相关的行才会导入数据馈送。  
  
    1.  使用报表中提供的列表框或组合框选择一个参数。  
  
    2.  单击 **“查看报表”** 更新数据。  
  
        > [!NOTE]  
        >  查看报表会将所选参数与数据馈送定义一起保存。  
  
     可以选择单击“高级”**** 为报表设置特定于提供程序的属性。  
  
6.  单击 **“测试连接”** 确保报表可以作为数据馈送。 或者，还可以单击 **“高级”** 以确认 **“嵌入式服务文档”** 属性包含指定数据馈送连接的嵌入的 XML。  
  
7.  单击 **“下一步”** 继续导入。  
  
8.  在 **“模拟信息”** 页中，指定刷新数据时 Analysis Services 将用于连接到数据源的凭据，然后单击 **“下一步”**。  
  
9. 在向导的 **“选择表和视图”** 页中，选中要作为数据导入的报表部件旁的复选框。  
  
     有些报表可以包含多种部件，包括表、列表或图形。  
  
10. 在 **“友好名称”** 框中，键入模型中要用于保存数据馈送的表的名称。  
  
     如果未指定名称，默认情况下，将使用 Reporting Services 控件的名称：例如，Tablix1、Tablix2。 建议您在导入过程中更改此名称，以便可以更容易地识别导入数据馈送的源。  
  
11. 单击 **“预览并筛选”** 检查数据并更改列选择。 您不能限制在报表数据馈送中导入的行，但可以通过清除相应的复选框来删除列。 单击“确定”。   
  
12. 在 **“选择表和视图”** 页上，单击 **“完成”**。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;支持的数据源](tabular-models/data-sources-supported-ssas-tabular.md)   
 [&#40;SSAS 表格&#41;支持的数据类型](tabular-models/data-types-supported-ssas-tabular.md)   
 [模拟 &#40;SSAS 表格&#41;](tabular-models/impersonation-ssas-tabular.md)   
 [&#40;SSAS 表格&#41;处理数据](process-data-ssas-tabular.md)   
 [&#40;SSAS 表格&#41;导入数据](import-data-ssas-tabular.md)  
  
  
