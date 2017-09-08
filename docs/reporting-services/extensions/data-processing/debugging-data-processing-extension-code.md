---
title: "调试数据处理扩展代码 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- debugging data processing extensions [Reporting Services]
- troubleshooting [Reporting Services], data processing extensions
- data processing extensions [Reporting Services], debugging
ms.assetid: e963e205-9ae0-446d-97df-028a1d2727d9
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 0b7ee42be2f3d54fc8fb19ab48b3b603e29669e2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="debugging-data-processing-extension-code"></a>调试数据处理扩展代码
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]提供多个调试工具，可帮助你分析你的数据处理扩展代码和在其中找到错误。 哪个工具效果最佳取决于您试图完成的任务。 此示例使用 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]。  
  
#### <a name="to-debug-your-data-processing-extension-code"></a>调试数据处理扩展插件代码  
  
1.  启动 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] 并打开数据处理扩展插件项目。  
  
2.  生成项目，并将数据处理扩展插件程序集以及随附的 .pdb 文件部署到报表设计器。 有关部署的详细信息，请参阅[如何： 将数据处理扩展插件部署到报表设计器](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)。  
  
3.  在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中打开新的报表项目，同时在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的一个单独窗口中让数据处理扩展插件代码处于打开状态。  
  
4.  导航到 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中包含数据处理扩展插件项目的窗口，并在代码中设置一些断点。  
  
5.  数据处理扩展项目窗口中仍处于活动状态，单击**附加到进程**上**调试**菜单。  
  
     **附加到进程**对话框随即打开。  
  
6.  从进程的列表中，选择报表项目对应的 devenv.exe 进程，然后单击**附加**。  
  
7.  定义报表数据源使用**报表数据**的报表项目的选项卡。 您最有可能使用一般性查询设计器来针对自定义数据源执行查询。 这将调用调试器并执行对应于断点的代码。  
  
8.  使用 F11 键分步执行代码。 有关使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 进行调试的详细信息，请参阅 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 文档。  
  
## <a name="see-also"></a>另请参阅  
 [部署数据处理扩展插件](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
