---
title: "第 2 课：指定连接信息 (Reporting Services) | Microsoft Docs"
ms.custom: ""
ms.date: "05/23/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
caps.latest.revision: 53
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 51
---
# 第 2 课：指定连接信息 (Reporting Services)
向“教程”项目添加报表之后，需要定义数据源，它是报表从关系数据库、多维数据库或其他资源访问数据所使用的连接信息。  
  
在本课中，将使用 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 示例数据库作为数据源。 本教程假定此数据库位于本地计算机上安装的默认 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]实例中。  
  
### 设置连接  
  
1.  在“报表数据”窗格中，单击“新建”，然后单击“数据源…”。  
如果“报表数据”窗格不可见，请单击“视图”菜单上的“报表数据”。  
  
   2.  在“名称”中，键入 *Adventureworks2014*。  
  
3.  确保已选中“嵌入连接”。  
  
4.  在“类型”中，选择 **Microsoft SQL Server**。  
  
5.  在“连接字符串”中，键入以下文本：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
该连接字符串假定 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、报表服务器和 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 数据库都已安装在本地计算机中，并且你拥有登录 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 数据库的权限。 如果 AdventureWorks2014 数据库不在本地计算机上，更改连接字符串，并将 loclahost 替换为数据库服务器实例名称。
   
  
 > [!NOTE]  
 > 如果使用的是带高级服务的 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 或命名实例，则连接字符串必须包括实例信息：  
 >   
 > `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
 >   
 > 有关连接字符串的详细信息，请参阅：  
 > *  [Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
    > * [“数据源属性”对话框 ->“常规”](../Topic/Data%20Source%20Properties%20Dialog%20Box,%20General.md)  
        
  
6.  在左窗格中单击“凭据”，然后单击“使用 Windows 身份验证(集成安全性)”。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] 会将 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 数据源添加到“报表数据”窗格中。  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## 下一个任务  
已成功定义了到 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 示例数据库的连接。 下一步，将创建报表。 请参阅[第 3 课：为表报表定义数据集 (Reporting Services)](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)。  
  
## 另请参阅  
[“数据源属性”对话框 ->“常规”](../Topic/Data%20Source%20Properties%20Dialog%20Box,%20General.md)  
[Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  
