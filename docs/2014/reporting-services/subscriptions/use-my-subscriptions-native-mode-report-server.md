---
title: 使用我的订阅 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], My Subscriptions page
- My Subscriptions page [Reporting Services]
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c1125792543e3a926ddb98e3d33e0f600328d232
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138777"
---
# <a name="use-my-subscriptions"></a>使用我的订阅
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 报表管理器包括**我的订阅**组织您的所有订阅在一个位置的页。 您可以使用“我的订阅”来查看、修改和删除现有订阅。 不过，您不能使用该页来创建订阅。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 本机模式|  
  
 在“我的订阅”中，您可以按文件夹、报表、说明、触发器、上次运行时间或状态来对订阅进行排序。 除了“上次运行时间”是按时间顺序排序之外，其他所有值都是按字母顺序排序的。  
  
 “我的订阅”仅显示您创建的订阅。 它不会列出其他用户拥有的订阅（即使您已添加为这些订阅的订阅者），也不会显示数据驱动订阅。  
  
 您既不能根据名称来搜索订阅，也不能根据触发器信息、状态信息等来搜索订阅。 有关详细信息，请参阅[Create，Modify，and 删除标准订阅&#40;在纯模式下的 Reporting Services&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)。  
  
## <a name="how-to-use-my-subscriptions"></a>如何使用“我的订阅”  
 可以通过报表管理器使用“我的订阅”。 若要访问“我的订阅”，请在报表管理器全局工具栏上单击 **“我的订阅”** 。  
  
## <a name="use-windows-powershell-to-list-mysubscriptions"></a>使用 Windows PowerShell 列出 MySubscription  
 ![与 PowerShell 相关的内容](../media/rs-powershellicon.jpg "PowerShell related content")  
  
 以下 PowerShell 脚本将返回当前用户的订阅和订阅属性的列表。 有关详细信息，请参阅 [ReportingService2010.ListMySubscriptions 方法](http://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx)。  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions  
  
```  
  
## <a name="see-also"></a>请参阅  
 [数据驱动订阅](data-driven-subscriptions.md)   
 [订阅和传递&#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [创建和管理本机模式报表服务器的订阅](../create-manage-subscriptions-native-mode-report-servers.md)  
  
  