---
title: rsServerConfigurationError - Reporting Services 错误 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 19778bce64e5779471e78b8c4305e1bd6315c0ac
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099212"
---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError - Reporting Services 错误
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|rsServerConfiguration|  
|事件源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|组件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|消息正文|报表服务器遇到配置错误。|  
  
## <a name="explanation"></a>说明  
 这是一个在报表服务器或报表创作工具具有无效配置设置时出现的常规错误。 通常该错误还附带另一条消息，该消息声明此错误的实际原因。  
  
 下面的列表汇总了可能的原因：  
  
-   找不到或无法读取 RSReportServer.config 或 RSReportDesigner.config 文件。  
  
-   这两个配置文件中有一个文件的 XML 元素丢失或无效。  
  
-   一个或多个 XML 元素的值丢失或无效。  
  
-   注册表设置无效。  
  
## <a name="user-action"></a>用户操作  
 如果该错误在您手动编辑配置文件后开始出现，请删除所做的更改并输入以前的值，或者如果您有备份，请还原先前的版本。  
  
 若要查看`rsServerConfiguration`错误附带的其他错误消息信息，请查看 Report Server 跟踪日志文件，这些文件位于 \Microsoft SQL Server\MSRS12。\<instancename > \reporting services\logfiles。 有关详细信息，请参阅 [Reporting Services 日志文件和源](../report-server/reporting-services-log-files-and-sources.md)。  
  
## <a name="internal-only"></a>仅内部  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置文件](../report-server/reporting-services-configuration-files.md)   
 [修改 Reporting Services 配置文件 (RSreportserver.config)](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
