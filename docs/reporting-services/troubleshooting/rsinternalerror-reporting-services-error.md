---
title: "rsInternalError - Reporting Services 错误 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: rsInternalError
ms.assetid: 52613d52-fc78-4870-93f0-7d393ab9c335
caps.latest.revision: "23"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 95f0e2c76aac661977ba0eedac84125c5b1e1888
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="rsinternalerror---reporting-services-error"></a>rsInternalError - Reporting Services 错误
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|rsInternalError|  
|事件源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|组件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|消息正文|报表服务器上出现内部错误。 有关详细信息，请参阅错误日志。|  
  
## <a name="explanation"></a>解释  
 这是一种一般性错误消息，后面通常跟着可提供详细信息的更具说明性的错误。  
  
 内部错误不常见。 如果出现此错误，可以查看报表服务器跟踪日志以了解详细信息。 此外，如果是以本地管理员的身份在出现错误的计算机上运行，则可以查看调用堆栈以了解详细信息。  
  
## <a name="user-action"></a>用户操作  
 若要确定出现此消息的具体原因，请查看位于以下目录的报表服务器日志文件：\Microsoft SQL Server\MSRS12.\<实例名>\Reporting Services\LogFiles。 有关详细信息，请参阅 [Reporting Services 日志文件和源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
 若要查看调用堆栈，请右键单击出现错误的页，然后指向“查看源”。 必须在出现该错误的同一计算机上具有管理员权限，才可查看调用堆栈。  
  
 如果没有其他可用信息，请再次尝试请求。  
  
## <a name="internal-only"></a>仅内部  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
