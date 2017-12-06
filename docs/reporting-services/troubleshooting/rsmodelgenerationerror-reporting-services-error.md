---
title: "rsModelGenerationError - Reporting Services 错误 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
caps.latest.revision: "17"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b515623ec4067abeaa80c13f7843e9af88999480
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="rsmodelgenerationerror---reporting-services-error"></a>rsModelGenerationError - Reporting Services 错误
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|rsRenderingError|  
|事件源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|组件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|消息正文|生成模型时出错。 (rsModelGenerationError) (ReportingServicesLibrary) %1|  
  
## <a name="explanation"></a>解释  
 不能生成报表模型。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 SP1 及更早版本中，如果 System.Data.DataSet 对象不能处理数据库架构中的表或关系（例如，如果在某个表中的同一列上定义两个外键），则最有可能发生此错误。  
  
## <a name="user-action"></a>用户操作  
 若要确定导致出现此消息的具体原因，请查看报表服务器日志文件，该文件位于 \Microsoft SQL Server\\<SQL Server Instance\>\Reporting Services\LogFiles。  
  
## <a name="internal-only"></a>仅内部  
  
