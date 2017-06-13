---
title: "第 3 课： 定义数据驱动订阅 |Microsoft 文档"
ms.custom: 
ms.date: 05/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
caps.latest.revision: 50
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1ae87a509d3d5d1eb55645408b63f8267498efbd
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>Lesson 3: Defining a Data-Driven Subscription
在本 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 教程课程中，将使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Web 门户数据驱动订阅页来连接到订阅数据源，生成一个检索订阅数据的查询，然后将结果集映射到报表和传递选项。  
  
> [!NOTE]  
> 在开始前，请确认“[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理”服务正在运行。 如果该代理服务未运行，则无法保存订阅。  一种验证方法是打开 [SQL Server 配置管理器](../relational-databases/sql-server-configuration-manager.md)。
本课程假设您已经完成了第 1 课和第 2 课，并且报表数据源使用存储的凭据。  有关详细信息，请参阅 [第 2 课：修改报表数据源属性](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)  
  
## <a name="bkmk_startwizard"></a>启动数据驱动订阅向导  
  
1.  在 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] Web 门户中，单击“主文件夹”，然后导航到包含“Sales Orders”报表的文件夹。  
  
2.  在报表的上下文菜单“ssrs_tutorial_datadriven_reportmenu”![](../reporting-services/media/ssrs-tutorial-datadriven-reportmenu.png)中，单击“管理”，然后单击左窗格中的“订阅”。  
  
3.  单击“+ 新建订阅”。 如果看不到此按钮，则说明您不具备“内容管理员”权限。 
  
## <a name="define-a-description"></a>定义说明  
1.  在说明中键入 **销售订单传递** 。
## <a name="type"></a>类型
1.  单击“数据驱动订阅”。  
## <a name="schedule"></a>计划
1. 在“计划”部分中，单击“报表特定计划”。
2. 单击“编辑计划”。
3.  在 **“计划详细信息”**中，单击 **“一次”**。  
4.  将开始时间指定为当前时间的前几分钟。  
5.  单击 **“应用”**。
## <a name="destination"></a>目标  
1.  在“目标”部分中，选择“Windows 文件共享”作为传递方法。  

## <a name="dataset"></a>数据集
1. 单击“编辑数据集”。
2. 选择 **“自定义数据源”**。
3. 选择“Microsoft SQL Server”作为数据源“连接”类型。
4. 在“连接字符串”中，键入以下连接字符串。 *Subscribers* 是在第 1 课中创建的数据库。 
  
    ```  
    data source=localhost; initial catalog=Subscribers
    ```
    
 ## <a name="credentials"></a>凭据
 1. 单击“使用以下凭据”。
 2. 选择“Windows 用户名和密码”。
 3.  在 **“用户名”** 和 **“密码”**中，键入您的域用户名和密码。 请在指定 **“用户名”**时同时包括域和用户帐户。
     > [!NOTE]  
    > 用于连接到订阅服务器数据源的凭据不会传递回 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 如果以后修改了该订阅，则必须重新键入连接到该数据源所用的密码。
## <a name="query"></a>Query      
1.  在查询框中，键入以下查询：  
  
    ```  
    Select * from OrderInfo  
    ```  
  
2.  指定 30 秒的超时。  
  
3.  单击“验证查询”，然后单击“应用”。
## <a name="delivery-options"></a>传递选项
填写以下值：

参数  |值源  | 值/字段  
---------|---------|---------
**文件名**     |从数据集获取值 | 订单     
**路径**     | 输入值  | 在“值”中，键入拥有写入权限的公共文件共享的名称（例如， `\\mycomputer\public\myreports`）。 
**呈现格式** | 从数据集获取值 | 格式
**写入模式**| 输入值| 自动增加    
**文件扩展名** |输入值 |True
**“用户名”** | 输入值 | 键入您的域用户帐户。 按以下格式输入：\<域 >\\\<帐户 >。 用户帐户需要对配置的路径具有权限。 
**“密码”** | 输入值 | 键入密码

## <a name="report-parameters"></a>报表参数
 1. 在“OrderNumber”字段中，选择“从数据集获取值”。 在“值”中，选择 **Order**。 
 2. 单击“创建订阅”。
   
## <a name="next-steps"></a>后续步骤  
订阅运行时，将有四个报表文件（分别属于 *Subscribers* 数据源中的各订单）发送到指定的文件共享中。 每个发送的报表在数据（数据应当是订单特定的）、呈现格式和文件格式方面都将是唯一的。 可以打开共享文件夹中的每一个报表以验证是否每个版本都是根据您定义的订阅选项来自定义的。  
  
![由订阅创建的文件的列表](../reporting-services/media/ssrs-tutorial-datadriven-subscription-filelist.gif "由订阅创建的文件的列表")  
  
Web 门户中的“订阅”页将包含订阅的“上次运行时间”日期和“状态”。 
**注意：** 在订阅运行后刷新该页可查看更新后的信息。  
    
![订阅结果在报表管理器](../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png "订阅结果在报表管理器")  
  
此步骤会结束“定义数据驱动订阅”教程。   
  
## <a name="see-also"></a>另请参阅  
[订阅和传递 (Reporting Services)](../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
[数据驱动订阅](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[创建、修改和删除数据驱动订阅](../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)  
[使用外部数据源提供订阅方数据（数据驱动订阅）](../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  
  


