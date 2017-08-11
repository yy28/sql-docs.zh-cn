---
title: "使用我的订阅 （本机模式报表服务器） |Microsoft 文档"
ms.custom: 
ms.date: 07/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], My Subscriptions page
- My Subscriptions page [Reporting Services]
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bc870d25cc341f84909e595cde4a411fecbf6603
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="use-my-subscriptions-native-mode-report-server"></a>使用我的订阅（本机模式报表服务器）
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 门户包括**我的订阅**组织您的所有订阅在一个位置的页。 你可以使用*我的订阅*若要查看、 修改、 启用、 禁用和删除现有订阅。 不过，您不能使用该页来创建订阅。  “我的订阅”仅显示您创建的订阅。 它不会列出其他用户拥有的订阅（即使您已添加为这些订阅的订阅者），也不会显示数据驱动订阅。
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式|  
  
搜索字段会动态筛选订阅列表。你既不能根据名称来搜索订阅，也不能根据触发器信息、状态信息等来搜索订阅。 有关详细信息，请参阅 [创建和管理本机模式报表服务器的订阅](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)。
  
## <a name="to-open-the-my-subscriptions-page"></a>打开“我的订阅”页  
1. 打开 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web 门户。
2. 单击“设置” ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) 在工具栏。
3. 单击“我的订阅”。

有关详细信息，请参阅 [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md)。

## <a name="use-windows-powershell-to-list-mysubscriptions"></a>使用 Windows PowerShell 列出 MySubscription  
 ![PowerShell 相关内容](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相关内容")  
  
 以下 PowerShell 脚本将返回当前用户的订阅和订阅属性的列表。 有关详细信息，请参阅 [ReportingService2010.ListMySubscriptions 方法](http://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx)。  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions

```  
  
## <a name="see-also"></a>另请参阅  
 [数据驱动订阅](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [订阅和传递 &#40;Reporting Services &#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [old_Create 和管理本机模式报表服务器的订阅](http://msdn.microsoft.com/en-us/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)  
  
  

