---
title: "rsInternalError-Reporting Services 错误 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rsInternalError
ms.assetid: 52613d52-fc78-4870-93f0-7d393ab9c335
caps.latest.revision: 23
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7265597c2376d62b6d3e42c55c8d87e45f6d869e
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

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
 若要确定此消息的具体原因，请查看位于 \Microsoft SQL Server\MSRS12 报表服务器日志文件。\<instancename > \Reporting Services\LogFiles。 有关详细信息，请参阅 [Reporting Services 日志文件和源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
 若要查看调用堆栈，请右键单击出现错误的页，然后指向“查看源”。 必须在出现该错误的同一计算机上具有管理员权限，才可查看调用堆栈。  
  
 如果没有其他可用信息，请再次尝试请求。  
  
## <a name="internal-only"></a>仅内部  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
