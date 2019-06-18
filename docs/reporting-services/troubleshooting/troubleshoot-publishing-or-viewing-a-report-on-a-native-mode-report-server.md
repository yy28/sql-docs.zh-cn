---
title: 对在本机模式报表服务器上发布或查看报表进行故障排除 | Microsoft Docs
ms.date: 02/28/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: df7720a1-d178-45bb-8d6f-63e208cae7fe
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6e3a96e3eef90778b0e7877b88ba79cb4e0dd43e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573862"
---
# <a name="troubleshoot-publishing-or-viewing-a-report-on-a-native-mode-report-server"></a>对在本机模式报表服务器上发布或查看报表进行故障排除
  
  
  
将报表发布或上载到配置为本机模式的报表服务器时，可能会看到特定于在该报表服务器上查看报表的问题。 使用本主题可以帮助解决这些问题。   
  
## <a name="why-am-i-being-prompted-for-credentials-when-i-publish-a-report"></a>为什么在发布报表时提示我输入凭据？  
若要将报表部署到报表服务器，必须指定服务器的地址。 可能会看到“Reporting Services 登录名”对话框，该对话框提示您输入凭据。   
  
未正确指定报表服务器名称  
  
  
向本机模式下的报表服务器部署报表时，常见的错误是指定报表文件夹的名称而不是报表服务器的名称。   
  
验证报表服务器 URL 是否是报表服务器的地址（例如， `https://localhost/reportserver`），而不是报表管理器虚拟目录的地址（例如， `https://localhost/reports`）。 如果你已为报表服务器指定与默认端口号 80 不同的端口号，则必须在报表服务器地址（例如， `https://localhost:81/reportserver`）中指定该端口号。   
  
 ## <a name="nothing-happens-when-i-toggle-items-in-my-published-report"></a>在已发布的报表中切换项时，无任何反应。  
  在本地预览中查看报表时，可在该报表中切换项，以及显示或隐藏这些项。 将报表发布到报表服务器后查看该报表时，切换项无法正常使用。   
  
\<报表服务器名称> 包含下划线 (_)  
  
如果运行报表时没有错误，但切换项不能正常使用（例如，单击展开图标 (+) 后没有反映），请检查承载报表服务器的计算机的名称。 如果计算机名称包含下划线，则切换项将无法正常使用。 这是一个已知问题。 目前没有解决方法。   
  
若要在运行报表时使用切换项，必须使用名称中没有下划线字符的计算机。  
  
## <a name="images-and-charts-do-not-load-when-i-use-run-as-and-a-browser-to-run-my-report"></a>使用“运行身份”和浏览器运行报表时不加载图像和图表。  
在不同的安全上下文运行报表管理器时，可能看不到报表中的所有报表项。   
  
### <a name="insufficient-permissions-on-internet-temporary-file-folders"></a>对 Internet 临时文件文件夹的权限不足  
  
在某些情况下，使用报表管理器查看包含图表或图像的已发布报表时，可能看不到这些报表项。 例如，使用 Microsoft Windows **Run As** 命令通过不同的安全性上下文查看报表时，你可能无权访问报表服务器在其中将图表和图像作为 Internet 临时文件进行缓存的文件夹。   
  
请验证您是否有权访问包含缓存文件的文件夹。   
    
## <a name="see-also"></a>另请参阅  
[Reporting Services 和 Power View 的浏览器支持](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[错误和事件 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Reporting Services 报表的数据检索问题疑难解答](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Reporting Services 订阅和传递的疑难解答](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

