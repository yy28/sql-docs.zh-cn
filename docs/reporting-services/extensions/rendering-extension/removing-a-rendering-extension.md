---
title: "删除呈现扩展插件 |Microsoft 文档"
ms.custom: 
ms.date: 03/18/2017
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
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: 38
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 58e9d46c17b300cda365e8b42d6442e00ffab0b9
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="removing-a-rendering-extension"></a>删除呈现扩展插件
  若要删除[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]呈现扩展插件时，只需删除**扩展**从 rsreportserver.config 文件，位于你呈现扩展插件的元素**%ProgramFiles%\Microsoft SQL Server\MSRS10_50。\<实例名称 > \Reporting Services\ReportServer**文件夹。 如果为报表设计器以及报表服务器进行条目，请删除**扩展**元素从[RSReportDesigner Configuration File](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md)以及。 在删除配置信息之后，该呈现扩展插件对于该组件将不再可用。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置文件](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [实现的呈现扩展插件](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [呈现扩展概述](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [实现 IRenderingExtension 接口](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [有关扩展的安全注意事项](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [部署呈现扩展插件](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  
