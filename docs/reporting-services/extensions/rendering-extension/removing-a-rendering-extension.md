---
title: "删除呈现扩展插件 | Microsoft Docs"
ms.custom: 
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: "38"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0ac5e10f4ea1aa66a4acf38bd0c4b64c3eb8be72
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="removing-a-rendering-extension"></a>删除呈现扩展插件
  要删除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 呈现扩展插件，只需从 rsreportserver.config file, located in %ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<Instance Name>\Reporting Services\ReportServer 文件夹中删除呈现扩展插件的 Extension 元素即可。 如果为报表设计器以及报表服务器生成条目，则还需从 [RSReportDesigner 配置文件](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md)中删除 Extension 元素。 在删除配置信息之后，该呈现扩展插件对于该组件将不再可用。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置文件](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [实现呈现扩展插件](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [呈现扩展插件概述](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [实现 IRenderingExtension 接口](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [扩展插件的安全注意事项](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [部署呈现扩展插件](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  
