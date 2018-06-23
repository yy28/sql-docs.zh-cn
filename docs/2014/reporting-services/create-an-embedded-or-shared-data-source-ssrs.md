---
title: 创建嵌入或共享数据源 (SSRS) |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data sources [Reporting Services], creating
ms.assetid: b111a8d0-a60d-4c8b-b00a-51644b19c34b
caps.latest.revision: 40
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 28609edfbfc504d3949abb6a19f7f04098fde07b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018128"
---
# <a name="create-an-embedded-or-shared-data-source-ssrs"></a>创建嵌入数据源或共享数据源 (SSRS)
  报表数据源指定名称和连接信息。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支持两种类型的数据源，分别是嵌入数据源和共享数据源。 嵌入数据源在报表定义中定义并只由该报表使用。 共享数据源被定义为一个单独项并可由多个报表使用。 有关详细信息，请参阅[嵌入和共享数据连接或数据源&#40;报表生成器和 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)。  
  
 在报表生成器中，浏览到报表服务器或 SharePoint 站点并选择数据源，或者创建嵌入数据源。 不能在报表生成器中创建共享数据源。  
  
 在报表设计器中，可以创建共享数据源或嵌入数据源。 从报表数据窗格中，开始创建数据源引用，，然后选择**新建**选项。 在您创建数据源引用后，新的共享数据源将自动添加到解决方案资源管理器中的“共享数据源”文件夹下。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 您还可以直接在报表服务器或 SharePoint 站点上创建共享数据源。 有关详细信息，请参阅[创建、 删除或修改共享数据源&#40;报表管理器&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)或[创建和管理共享数据源&#40;Reporting Services SharePoint 集成模式下&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
### <a name="to-create-an-embedded-or-shared-data-source"></a>若要创建嵌入或共享数据源  
  
1.  在“报表数据”窗格的工具栏中，单击 **“新建”** ，然后单击 **“数据源”**。 此时将打开 **“数据源属性”** 对话框。  
  
    > [!NOTE]  
    >  如果“报表数据”窗格不可见，请单击“视图”菜单上的“报表数据”。  
  
2.  在 **“名称”** 文本框中，键入数据源的名称，或接受默认值。 此数据源名称在报表内部使用。 为便于识别，建议数据源名称包含在连接字符串中指定的数据库的名称。  
  
3.  对于嵌入的数据源，确认**嵌入连接**选择。  
  
    1.  从“类型”下拉列表中，选择一个数据源类型，例如“Microsoft SQL Server”或“OLE DB”。  
  
    2.  采用以下备选方案之一指定连接字符串：  
  
    -   直接在 **“连接字符串”** 文本框中键入连接字符串。 有关示例连接字符串的列表，请参阅[数据连接、 数据源和报表生成器中的连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)或[数据连接、 数据源和连接字符串在 Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
    -   单击表达式 (**fx** ) 按钮创建计算结果为连接字符串的表达式。 在 **“表达式”** 对话框的“表达式”窗格中，键入该表达式。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    -   单击 **“编辑”** 打开在步骤 2 中选择的数据源类型的 **“连接属性”** 对话框。  
  
         根据需要，在 **“连接属性”** 对话框中为该数据源类型填写字段。 连接属性包括数据源的类型、名称以及要使用的凭据。 在此对话框中指定值之后，单击 **“测试连接”** 以确保该数据源可用并且指定的凭据是正确的。 有关特定数据源类型的详细信息，请参阅[从外部数据源中添加数据 (SSRS)](report-data/add-data-from-external-data-sources-ssrs.md) 中的主题。  
  
4.  对于共享的数据源，确认**使用共享数据源引用**选择。  
  
    1.  单击 **“新建”**。 在 **“共享数据源属性”** 对话框中，执行步骤 2 和 3 创建新数据源。  
  
    2.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
         解决方案资源管理器的“共享数据源”文件夹中将显示新的共享数据源。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     数据源将显示在“报表数据”窗格中。 在“报表数据”窗格中，一个共享数据源将指向数据源定义。 在报表生成器中，数据源定义位于报表服务器或 SharePoint 站点上。 在报表设计器中，数据源定义是解决方案资源管理器中“共享数据源”文件夹下的一个文件。  
  
### <a name="to-import-an-existing-data-source-in-report-designer"></a>在报表设计器中导入现有数据源  
  
1.  在解决方案资源管理器中，右键单击报表服务器项目中的“共享数据源”文件夹，然后单击“添加现有项”。 此时将打开 **“添加现有项”** 对话框。  
  
2.  导航到一个现有报表定义共享数据源 (rds) 文件，然后单击“打开”。  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-convert-an-embedded-data-source-to-a-shared-data-source-in-report-designer"></a>在报表设计器中将嵌入数据源转换为共享数据源  
  
-   在报表数据窗格中，右键单击数据源，然后单击**将转换为共享数据源**。  
  
### <a name="to-convert-a-shared-data-source-to-an-embedded-data-source-in-report-builder"></a>在报表生成器中将共享数据源转换为嵌入数据源  
  
-   在报表数据窗格中，右键单击数据源并打开**数据源属性**。  
  
-   单击**嵌入连接**和完成前面过程中所述创建嵌入的数据源。  
  
## <a name="see-also"></a>请参阅  
 [在 Reporting Services 数据源中存储凭据](report-data/store-credentials-in-a-reporting-services-data-source.md)   
 [嵌入和共享数据连接或数据源&#40;报表生成器和 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [转换从数据源嵌入到共享&#40;报表生成器和 SSRS&#41;](report-data/convert-data-sources-report-builder-and-ssrs.md)   
 [将报表或模型绑定到共享的数据源&#40;SSRS&#41;](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [配置报表的数据源属性（报表管理器）](report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Reporting Services 支持的数据源&#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  