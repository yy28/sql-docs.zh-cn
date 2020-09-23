---
title: rsServerConfigurationError - Reporting Services 错误 | Microsoft Docs
description: 在此错误参考页中，了解事件 ID“rsServerConfigurationError”：报表服务器遇到配置错误。
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3076c0f00a358a1a2adbee57178561649e6a44c2
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395185"
---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError - Reporting Services 错误
    
## <a name="details"></a>详细信息  
  
|类别|值|  
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
  
 若要查阅 rsServerConfiguration 错误随附的其他错误消息信息，请查阅位于以下目录的报表服务器跟踪日志文件：\Microsoft SQL Server\MSRS12.\<instancename >\Reporting Services\LogFiles。 有关详细信息，请参阅 [Reporting Services 日志文件和源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
## <a name="internal-only"></a>仅内部  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置文件](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
