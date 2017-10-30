---
title: "调试传递扩展代码 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], debugging
- debugging delivery extensions [Reporting Services]
- troubleshooting [Reporting Services], delivery extensions
ms.assetid: a7d959da-5005-4a50-aca7-2cef36aa9947
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e2d2162167123c152cbbeb58739f25ee06ec692a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="debugging-delivery-extension-code"></a>调试传递扩展插件代码
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]提供多个调试工具，可帮助你分析你的传递扩展插件代码，然后在它找到错误。 哪个工具效果最佳取决于您试图完成的任务。 此示例使用 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]。  
  
#### <a name="to-debug-your-delivery-extension-code"></a>若要调试传递扩展插件代码  
  
1.  启动[!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]并打开传递扩展项目。  
  
2.  生成项目，并将传递扩展插件程序集以及随附的 .pdb 文件部署到报表服务器和报表管理器。 有关部署的详细信息，请参阅[Deploying a Delivery Extension](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)。  
  
3.  如果您编写了订阅用户界面以扩展报表管理器，请打开 Internet Explorer 并导航到报表管理器，同时在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中保持传递扩展插件代码处于打开状态。 如果没有为报表管理器部署订阅用户界面，则只需打开客户端应用程序，从中可以使用 SOAP API 调用传递扩展插件。  
  
4.  导航到 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 和传递扩展插件项目，并在代码中设置一些断点。  
  
5.  使用传递的扩展项目仍是活动的窗口中，单击**附加到进程**上**调试**菜单。  
  
     **附加到进程**对话框随即打开。  
  
6.  从进程的列表，选择 aspnet_wp.exe 进程 （或如果你的应用程序部署在 IIS 6.0 上 w3wp.exe），然后单击**附加**。  
  
7.  使用传递扩展插件定义新订阅。 您最可能使用报表管理器或 SOAP API。 这将调用调试器并执行对应于断点的代码。  
  
8.  你的代码使用单步调试**F11**密钥。 有关使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 进行调试的详细信息，请参阅 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 文档。  
  
## <a name="see-also"></a>另请参阅  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

