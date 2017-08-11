---
title: "第 2 课： 指定连接信息 (Reporting Services) |Microsoft 文档"
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
caps.latest.revision: 53
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4d0667dec1b59d5560ca24176634dddc5d6d8d18
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>第 2 课：指定连接信息 (Reporting Services)
添加后[!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)]分页报表到教程第 1 课中的项目，现在你需要定义*数据源*，这是报表使用从关系数据库、 多维数据库或另一个源访问数据的连接信息。  
  
在本课程中，你使用[!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]作为数据源的示例数据库。 本教程假定此数据库位于的默认实例[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]在本地计算机上安装。  
  
### <a name="to-set-up-a-connection"></a>设置连接  
  
1.  在**报表数据**窗格中，单击**新建**，然后单击**数据源**。  
如果“报表数据”窗格不可见，请单击“视图”菜单上的“报表数据”。  

    ![ssrs-table-tutorial-2-new-data-source](../reporting-services/media/ssrs-table-tutorial-2-new-data-source.png)
  
   2.  在**名称**，类型*AdventureWorks2014*。  
  
3.  确保已选中“嵌入连接”。  
  
4.  在**类型**，选择**Microsoft SQL Server**。  
  
5.  在**连接字符串**，键入以下命令：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
     该连接字符串假定 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、报表服务器和 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 数据库都已安装在本地计算机中，并且你拥有登录 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 数据库的权限。 如果你为 AdventureWorks2014 数据库不在本地计算机上，更改连接字符串，替换*localhost*替换为你的数据库服务器实例的名称。
  
     >[!NOTE]  
    >如果使用的是带高级服务的 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 或命名实例，则连接字符串必须包括实例信息：  
    >  
    >`Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
    >  
    >有关连接字符串的详细信息，请参阅： [Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
     
  
6.  在左窗格中单击“凭据”，然后单击“使用 Windows 身份验证(集成安全性)”。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]数据源**AdventureWorks2014**添加到**报表数据**窗格。  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## <a name="next-task"></a>下一个任务  
已成功定义了到 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 示例数据库的连接。 下一步，将创建报表。 请参阅[第 3 课： 定义数据集的表报表 &#40;Reporting Services &#41;](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md).  
  
## <a name="see-also"></a>另請參閱  
[Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  


