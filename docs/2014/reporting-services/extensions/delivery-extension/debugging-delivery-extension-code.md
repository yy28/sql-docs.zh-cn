---
title: 调试传递扩展插件代码 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], debugging
- debugging delivery extensions [Reporting Services]
- troubleshooting [Reporting Services], delivery extensions
ms.assetid: a7d959da-5005-4a50-aca7-2cef36aa9947
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0d289b3d4c4177ed885a3153bb758d0052286bec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63164332"
---
# <a name="debugging-delivery-extension-code"></a>调试传递扩展插件代码
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)]提供了一些调试工具，可帮助你分析传递扩展插件代码和查找其中的[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]错误。 哪个工具效果最佳取决于您试图完成的任务。 此示例使用 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]。  
  
#### <a name="to-debug-your-delivery-extension-code"></a>调试传递扩展插件代码  
  
1.  启动 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] 并打开传递扩展插件项目。  
  
2.  生成项目，并将传递扩展插件程序集以及随附的 .pdb 文件部署到报表服务器和报表管理器。 有关部署的详细信息，请参阅[部署传递扩展插件](deploying-a-delivery-extension.md)。  
  
3.  如果您编写了订阅用户界面以扩展报表管理器，请打开 Internet Explorer 并导航到报表管理器，同时在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中保持传递扩展插件代码处于打开状态。 如果没有为报表管理器部署订阅用户界面，则只需打开客户端应用程序，从中可以使用 SOAP API 调用传递扩展插件。  
  
4.  导航到 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 和传递扩展插件项目，并在代码中设置一些断点。  
  
5.  在传递扩展插件项目的窗口仍保持活动状态的同时，在“调试”菜单中单击“附加到进程”********。  
  
     “附加到进程”对话框会打开****。  
  
6.  从进程列表中，选择 aspnet_wp.exe 进程（如果应用程序是在 IIS 6.0 中部署的，请选择 w3wp.exe），然后单击“附加”****。  
  
7.  使用传递扩展插件定义新订阅。 您最可能使用报表管理器或 SOAP API。 这将调用调试器并执行对应于断点的代码。  
  
8.  使用**F11**键分步执行代码。 有关使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 进行调试的详细信息，请参阅 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 文档。  
  
## <a name="see-also"></a>另请参阅  
 [实现传递扩展插件](implementing-a-delivery-extension.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  
