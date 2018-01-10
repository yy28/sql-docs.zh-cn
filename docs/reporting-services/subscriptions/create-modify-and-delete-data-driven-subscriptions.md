---
title: "创建、修改和删除数据驱动订阅 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: subscriptions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query-based subscriptions [Reporting Services]
- queries [Reporting Services], data-driven subscriptions
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: 0ba2093e-9393-4eb6-af06-9da10988cfaf
caps.latest.revision: "51"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 92aab81d1e8bb487b3cbf671c4e15034abe09341
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="create-modify-and-delete-data-driven-subscriptions"></a>创建、修改和删除数据驱动订阅
  数据驱动订阅是一种基于查询的订阅，可以在运行时获取用于处理该订阅的数据值。 当触发订阅时，会处理一个查询以获取有关收件人、报表传递选项、呈现格式和参数设置的最新信息。 将查询结果与订阅定义相结合，以创建动态订阅，该订阅使用了已在雇员数据库、客户数据库或任何其他数据库（包含可用作订阅服务器数据的信息）中维护的数据。  
  
 若要创建新的数据驱动订阅或修改现有订阅，请使用报表管理器中的“创建数据驱动订阅”页。 这些页面将引导您完成创建或修改订阅的每一个步骤。 若要在创建订阅后访问该订阅，请使用“我的订阅”页和报表的“订阅”列表。 若要了解如何创建数据驱动订阅，请参阅[创建数据驱动订阅（SSRS 教程）](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)。  
  
 本主题内容：  
  
-   [管理和删除数据驱动订阅](#bkmk_manage_and_delete)  
  
-   [创建和修改数据驱动订阅](#bkmk_create_and_modify)  
  
-   [定义用于检索订阅信息的查询](#bkmk_define_query)  
  
-   [运行订阅](#bkmk_run_subscription)  
  
##  <a name="bkmk_manage_and_delete"></a> 管理和删除数据驱动订阅  
 不能通过报表管理器的“管理作业”页来停止或删除正在进行的数据驱动订阅。 因此，使用共享计划触发数据驱动订阅是有利的。 在这种情况下，如果要暂时禁止处理某个订阅，只需暂停触发该订阅的计划即可。 有关详细信息，请参阅 [（旧）创建和管理本机模式报表服务器的订阅](http://msdn.microsoft.com/en-us/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)。  
  
 若要删除数据驱动订阅，请从“我的订阅”页或报表的“订阅”页中选定该订阅，再单击 **“删除”**。  
  
 有关如何取消数据驱动订阅的说明，请参阅 [管理运行中的进程](../../reporting-services/subscriptions/manage-a-running-process.md)。  
  
##  <a name="bkmk_create_and_modify"></a> 创建和修改数据驱动订阅  
 若要创建数据驱动订阅，请选择一个使用存储的凭据或不使用任何凭据的报表。 在您创建数据驱动订阅时，请考虑将命名约定用于说明字段，以便可以轻松地将标准说明与数据驱动说明区分开来。  
  
#### <a name="to-create-a-data-driven-subscription-native-mode"></a>创建数据驱动订阅（本机模式）  
  
1.  在报表管理器中，导航到包含该报表的文件夹，将鼠标悬停在该报表上，打开选项菜单并单击 **“管理”**。  
  
2.  单击 **“订阅”** 选项卡。  
  
3.  单击 **“新建数据驱动订阅”** 按钮。  
  
#### <a name="to-create-a-data-driven-subscription-sharepoint-mode"></a>创建数据驱动订阅（SharePoint 模式）  
  
1.  在 SharePoint 文档库中，将鼠标悬停在该报表上，打开选项菜单并单击 **“管理订阅”**。  
  
2.  单击 **“添加数据驱动订阅”**。  
  
#### <a name="to-modify-an-existing-data-driven-subscription-native-mode"></a>修改现有的数据驱动订阅（本机模式）  
  
1.  在报表管理器中，导航到包含该报表的文件夹，将鼠标悬停在该报表上，打开选项菜单并单击 **“管理”**。  
  
2.  单击 **“订阅”** 选项卡。也可以单击报表管理器顶部的“我的订阅”链接  
  
3.  选择要修改的订阅。 以下图标表示数据驱动订阅：![数据驱动订阅图标](../../reporting-services/subscriptions/media/hlp-16subscriptiondd.gif "Data-driven subscription icon")  
  
#### <a name="to-modify-an-existing-data-driven-subscription-sharepoint-mode"></a>修改现有的数据驱动订阅（SharePoint 模式）  
  
1.  在 SharePoint 文档库中，将鼠标悬停在该报表上，打开选项菜单并单击 **“管理订阅”**。  
  
2.  选择要修改的订阅。  
  
> [!NOTE]  
>  您可以修改任何已指定的值。 除了用来访问订阅服务器数据存储区的密码外，所有值都以最初创建时的形式显示。 每次修改第二页或任何后续页上的值时，都必须重新键入密码。  
  
 创建数据驱动订阅之前，请确保满足下列要求：  
  
-   **报表要求**。 报表必须使用已存储的凭据或不使用任何凭据在运行时检索数据。 不能订阅使用模拟凭据或委托凭据连接至外部数据源的报表；处理订阅时将无法使用创建或拥有订阅的用户的凭据。 已存储的凭据可以是 Windows 帐户或数据库用户帐户。 有关详细信息，请参阅 [Specify Credential and Connection Information for Report Data Sources](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)。  
  
     无法订阅使用了作为数据源的模型或包含模型项安全设置的模型的报表生成器报表。 此限制仅适用于使用模型项安全性的报表。  
  
     对于包含 `User!UserID` 表达式的报表，您无法创建数据驱动订阅。  
  
-   **数据要求**。 必须具有包含订阅服务器数据的可访问外部数据源。  
  
-   **用户要求**。 订阅的作者必须具有“管理报表”和“管理所有订阅”的权限。 有关项级任务权限的详细信息，请参阅 [任务和权限](../../reporting-services/security/tasks-and-permissions.md)。 作者还须具有访问包含订阅服务器数据的外部数据源所需的凭据。  
  
##  <a name="bkmk_define_query"></a> 定义用于检索订阅信息的查询  
 数据驱动订阅必须指定一个用于检索订阅服务器数据的查询或命令。 查询应为每个订阅服务器生成一行。 如果使用的是电子邮件传递扩展插件，则查询应为每个订阅服务器返回一个有效的电子邮件别名。 所执行的传递的数量取决于查询所返回的行数。 如果行集中包含 10,000 行，则该订阅将传递 10,000 个报表。  
  
 如果执行查询很耗时，则可以增加超时值以允许进行其他处理。  
  
 必须在此步骤中对查询进行验证才能继续。 验证操作并不处理查询，但它的确会返回行集中所有列的列表，以便可以在后续选择中引用这些列。 如果查询未能通过验证，则将无法继续操作。 如果查询语法不正确或者如果与数据源的连接无效，则查询将无法通过验证。 可使用 **“上一步”** 按钮更正数据源。  
  
##  <a name="bkmk_run_subscription"></a> 运行订阅  
 必须指定处理订阅的条件。 可以指定一个计划，也可以触发该订阅以便与对报表执行快照的更新保持一致。 处理数据驱动订阅的方式与处理标准订阅的方式相同。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理本机模式报表服务器的订阅](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [订阅和传递 (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [（旧）创建和管理本机模式报表服务器的订阅](http://msdn.microsoft.com/en-us/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)   
 [“订阅”页（报表管理器）](http://msdn.microsoft.com/library/cf3a6bd0-e0b2-4875-a532-63ef34cfa860)   
 [“我的订阅”页（报表管理器）](http://msdn.microsoft.com/library/491a85a3-f323-4155-a0a8-de2779899995)  
  
  
