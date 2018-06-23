---
title: 第 3 课：定义数据驱动订阅 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 136335f0e56433a9478ddee37d0b8f585564776e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128036"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>Lesson 3: Defining a Data-Driven Subscription
  在本课程中，您将使用数据驱动订阅页来连接订阅数据源，生成一个检索订阅数据的查询，然后将结果集映射到报表和传递选项。  
  
> [!NOTE]  
>  开始操作之前，请确认 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理服务正在运行。 如果该代理服务未运行，则无法保存订阅。  
  
 本课程假设您已经完成了第 1 课和第 2 课，并且报表数据源使用存储的凭据。  有关详细信息，请参阅 [第 2 课：修改报表数据源属性](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)  
  
 本主题内容：  
  
-   [启动数据驱动订阅向导](#bkmk_startwizard)  
  
-   [步骤 1-定义说明](#bkmk_definesubscription)  
  
-   [步骤 2-定义了一个连接到订阅服务器数据源](#bkmk_defineconnectiontosubscriber)  
  
-   [步骤 3-定义检索订阅服务器数据的查询](#bkmk_definequery)  
  
-   [步骤 4-设置传递选项](#bkmk_set_deliveryoptions)  
  
-   [第 5 步-配置参数值以改变报表输出](#bkmk_configure_parameter)  
  
-   [步骤 6-计划订阅](#bkmk_schedule_subscription)  
  
##  <a name="bkmk_startwizard"></a> 启动数据驱动订阅向导  
  
1.  在报表管理器中，单击 **“主文件夹”**，导航到包含 **Sales Orders** 报表的文件夹。  
  
2.  在该报表的上下文菜单中，单击 **“管理”**，然后单击 **“订阅”** 选项卡。  
  
3.  单击**新数据驱动订阅**。 如果看不到此按钮，则说明您不具备“内容管理员”权限。  
  
##  <a name="bkmk_definesubscription"></a> 步骤 1-定义说明  
  
1.  在说明中键入 **销售订单传递** 。  
  
2.  为 **“指定通知收件人的方式”** 选择 **“Windows 文件共享”**。  
  
3.  选中 **“仅为此订阅指定”**，然后单击 **“下一步”**。  
  
##  <a name="bkmk_defineconnectiontosubscriber"></a> 步骤 2-定义了一个连接到订阅服务器数据源  
  
1.  选择 **“Microsoft SQL Server”** 作为数据源类型。  
  
2.  在“连接字符串”中，键入以下连接字符串：  
  
    ```  
    data source=localhost; initial catalog=Subscribers  
    ```  
  
    > [!NOTE]  
    >  订阅服务器是你在第 1 课中创建的数据库。  
  
3.  单击 **“安全存储在报表服务器中的凭据”**。  
  
4.  在 **“用户名”** 和 **“密码”** 中，键入您的域用户名和密码。 请在指定 **“用户名”** 时同时包括域和用户帐户。  
  
    > [!NOTE]  
    >  用于连接到订阅服务器数据源的凭据不会传递回 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 如果以后修改了该订阅，则必须重新键入连接到该数据源所用的密码。  
  
5.  选择 **“在与数据源建立连接时用作 Windows 凭据”**，再单击 **“下一步”**。  
  
##  <a name="bkmk_definequery"></a> 步骤 3-定义检索订阅服务器数据的查询  
  
1.  在查询框中，键入以下查询：  
  
    ```  
    Select * from OrderInfo  
    ```  
  
2.  指定 30 秒的超时。  
  
3.  单击 **“验证”**，再单击 **“下一步”**。  
  
##  <a name="bkmk_set_deliveryoptions"></a> 步骤 4-设置传递选项  
  
1.  对于 **“文件名”**，请选择 **“从数据库获取该值”**。 选择字段 **Order**。  
  
2.  对于 **“路径”**，请选择 **“指定静态值”**。 在设置值中，键入为其具有写入权限的公共文件共享的名称 (例如， `\\mycomputer\public\myreports`)。  
  
3.  对于 **“呈现格式”**，请选择 **“从数据库获取该值”**。 选择 **“格式”**。  
  
4.  对于 **“写入模式”**，请选择 **“指定静态值”** 并且选择 **AutoIncrement**。  
  
5.  对于 **“文件扩展名”**，请选择 **“指定静态值”** 并且选择 **True**。  
  
6.  对于 **“用户名”**，请选择 **“指定静态值”**。 键入您的域用户帐户。 按以下格式输入： `<domain>\<account>`。 用户帐户需要对您在前面的步骤中配置的路径具有权限。  
  
7.  对于 **“密码”**，请选择 **“指定静态值”**。 键入您的密码。 请务必仔细键入密码。 向导不会对密码进行验证。  
  
8.  单击 **“下一步”**。  
  
##  <a name="bkmk_configure_parameter"></a> 第 5 步-配置参数值以改变报表输出  
  
1.  对于 **OrderNumber**，请选择 **“从数据库获取该值”**。 在“值”中，选择 **Order**。 单击 **“下一步”**。  
  
##  <a name="bkmk_schedule_subscription"></a> 步骤 6-计划订阅  
  
1.  单击 **“根据为此订阅创建的计划”**，再单击 **“下一步”**。  
  
2.  在 **“计划详细信息”** 中，单击 **“一次”**。  
  
3.  将开始时间指定为当前时间的前几分钟。  
  
4.  单击 **“完成”**。  
  
## <a name="next-steps"></a>后续步骤  
 订阅运行时，将有四个报表文件（分别属于 *Subscribers* 数据源中的各订单）发送到指定的文件共享中。 每个发送的报表在数据（数据应当是订单特定的）、呈现格式和文件格式方面都将是唯一的。 可以打开共享文件夹中的每一个报表以验证是否每个版本都是根据您定义的订阅选项来自定义的。  
  
 ![按订阅创建的文件列表](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-filelist.gif "List of files created by the subscription")  
  
 报表管理器中的订阅页将包含订阅的 **“上次运行时间”** 日期和 **“状态”** 。  
  
> [!NOTE]  
>  在订阅运行后刷新该页可查看更新后的信息。  
  
 ![报表管理器中的订阅结果](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.gif "Subscription results in Report Manager")  
  
 此步骤将结束“定义数据驱动订阅”教程。 若要了解有关其他详细[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]教程，请参阅[Reporting Services 教程&#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [创建数据驱动订阅（SSRS 教程）](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [订阅和传递&#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [数据驱动订阅](subscriptions/data-driven-subscriptions.md)   
 [创建、 修改和删除数据驱动订阅](subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [使用外部数据源提供订阅方数据&#40;数据驱动订阅&#41;](subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  