---
title: Windows 应用程序日志 | Microsoft Docs
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
- Windows application logs [Reporting Services]
- logs [Reporting Services], Windows application logs
- application logs [Reporting Services]
ms.assetid: 742fd00e-aa6c-4c8a-b58f-c03c489b1699
caps.latest.revision: 31
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c8fab15175eddb015bac7bd96d97bceba1fbd076
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016087"
---
# <a name="windows-application-log"></a>Windows 应用程序日志
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将事件消息写入 Windows 应用程序日志。 您可以使用写入应用程序日志的消息信息，找出在本地系统上运行的报表服务器应用程序生成的事件。  
  
## <a name="viewing-report-server-events"></a>查看报表服务器事件  
 使用事件查看器可以查看日志文件并筛选其中包含的消息。 有关事件消息的详细信息，请参阅[错误和事件参考&#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)。 有关 Windows 应用程序日志或事件查看器的详细信息，请参阅 Windows 产品文档。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供以下三个事件源：  
  
-   报表服务器（报表服务器 Windows 服务）  
  
-   报表管理器  
  
-   计划和传递处理器  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 未提供关闭报表服务器的应用程序事件记录的方法，也无法控制记录哪些事件。 描述报表服务器事件日志记录的架构是固定的。 您不能将架构扩展到可以支持自定义事件。  
  
 下表对报表服务器写入应用程序事件日志的事件类型进行了说明：  
  
|事件类型|Description|  
|----------------|-----------------|  
|信息|描述成功操作的事件（例如，报表服务器服务的启动时间）。|  
|警告|指示潜在问题的事件（如磁盘空间不足）。|  
|错误|描述重要问题的事件（如服务未能启动）。|  
|审核成功|描述成功登录的安全性事件。|  
|审核失败|登录失败时记录的事件。|  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 日志文件和来源](../report-server/reporting-services-log-files-and-sources.md)   
 [错误和事件参考&#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  