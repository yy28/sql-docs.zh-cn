---
title: 第 2 课：指定连接信息 (Reporting Services)| Microsoft Docs
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 381192f80128ca3bd2ebade55dc539137c4bc9bd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47805605"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>第 2 课：指定连接信息 (Reporting Services)
向第 1 课中的“教程”项目添加 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 分页报表后，现在需要定义数据源，它是报表从关系数据库、多维数据库或另一个源访问数据所使用的连接信息。  
  
在本课中，使用 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 示例数据库作为数据源。 本教程假定此数据库位于本地计算机上安装的默认 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例中。  
  
### <a name="to-set-up-a-connection"></a>设置连接  
  
1.  在“报表数据”窗格中，单击“新建”，然后单击“数据源”。  
如果“报表数据”窗格不可见，请单击“视图”菜单上的“报表数据”。  

    ![ssrs-table-tutorial-2-new-data-source](../reporting-services/media/ssrs-table-tutorial-2-new-data-source.png)
  
   2.  在“名称”中，键入 Adventureworks2014。  
  
3.  确保已选中“嵌入连接”。  
  
4.  在“类型”中，选择 Microsoft SQL Server。  
  
5.  在“连接字符串”中，键入以下文本：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
     该连接字符串假定 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、报表服务器和 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 数据库都已安装在本地计算机中，并且你拥有登录 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 数据库的权限。 如果 AdventureWorks2014 数据库不在本地计算机上，更改连接字符串，并将 loclahost 替换为数据库服务器实例名称。
  
     >[!NOTE]  
    >如果使用的是带高级服务的 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 或命名实例，则连接字符串必须包括实例信息：  
    >  
    >`Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
    >  
    >有关连接字符串的详细信息，请参阅： [报表生成器中的数据连接、数据源和连接字符串](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
     
  
6.  在左窗格中单击“凭据”，然后单击“使用 Windows 身份验证(集成安全性)”。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] 将数据源 AdventureWorks2014 添加到“报表数据”窗格。  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## <a name="next-task"></a>下一个任务  
已成功定义了到 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 示例数据库的连接。 下一步，将创建报表。 请参阅[第 3 课：为表报表定义数据集 (Reporting Services)](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)。  
  
## <a name="see-also"></a>另请参阅  
[报表生成器中的数据连接、数据源和连接字符串](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  

