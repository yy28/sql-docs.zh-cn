---
title: 删除呈现扩展插件 | Microsoft Docs
description: 了解如何从 Reporting Services 删除呈现扩展插件，以使其不再可用于报表服务器和报表设计器。
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f71fceddd59141516453f9f392f8f913ba20cfad
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529433"
---
# <a name="removing-a-rendering-extension"></a>删除呈现扩展插件
  若要删除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 呈现扩展插件，只需从位于 %ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<Instance Name>\Reporting Services\ReportServer 文件夹的 rsreportserver.config 文件中删除呈现扩展插件的 Extension 元素即可 。 如果为报表设计器以及报表服务器生成条目，则还需从 [RSReportDesigner 配置文件](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md)中删除 Extension 元素****。 在删除配置信息之后，该呈现扩展插件对于该组件将不再可用。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置文件](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [实现呈现扩展插件](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [呈现扩展插件概述](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [实现 IRenderingExtension 接口](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [扩展插件的安全注意事项](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [部署呈现扩展插件](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  
