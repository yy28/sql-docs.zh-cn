---
title: 停止使用的 SQL Server 2014 中的 SQL Server Reporting Services 功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- discontinued functionality [Reporting Services]
- Reporting Services, backward compatibility
- Rsactivate.exe
- unsupported features [Reporting Services]
ms.assetid: d529cc96-3483-480b-9bfc-bd28b1d0ef52
caps.latest.revision: 47
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 971662bbb0b1c8b08507574d569418d065f6204a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201027"
---
# <a name="discontinued-functionality-to-sql-server-reporting-services-in-sql-server-2014"></a>SQL Server 2014 的 SQL Server Reporting Services 中停止使用的功能
  此主题介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中不再可用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。 此处不包括关于停止支持某些版本的操作系统或 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Services (IIS) 的声明。 有关系统先决条件的详细信息，请参阅[的硬件和软件要求安装 SQL Server 2014](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
 本主题内容：  
  
-   [SQL Server 2014 Reporting Services 中停止使用的功能](#bkmk_sql14)  
  
-   [SQL Server 2012 Reporting Services 中停止使用的功能](#bkmk_rc0)  
  
-   [SQL Server 2008 R2 Reporting Services 中停止使用的功能](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Reporting Services 停止使用的功能  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中没有已停止使用的 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 功能。  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Reporting Services 停止使用的功能  
 本节介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中停止使用的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 功能。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中没有已停止使用的 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 功能。  
  
##  <a name="bkmk_kj"></a> SQL Server 2008 R2 Reporting Services 中停止使用的功能  
 本部分介绍在停用[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]。  
  
> [!NOTE]  
>  因为 SQL Server 2008 R2 是 SQL Server 2008 的次版本升级，所以，我们建议您也查看 SQL Server 2008 部分的内容。  
  
### <a name="64-bit-platform-support"></a>64 位平台支持  
 在中启动[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]，则[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]组件不再支持运行 Windows Server 2003 或 Windows Server 2003 R2 的基于 Itanium 的服务器。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 继续以支持其他 64 位操作系统，包括 Windows Server 2008 for Itanium-Based Systems 和 Windows Server 2008 R2 for Itanium-Based Systems。 若要在 Windows Server 2003 或 Windows Server 2003 R2 的基于 Itanium 的系统版本上从具有 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 安装升级到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，您必须首先升级操作系统。  
  
### <a name="data-source-credentials-in-url-access"></a>URL 访问中的数据源凭据  
 URL 访问参数字符串*dsu:datasourcename = value*并*dsp:datasourcename = value*现已终止。 在早期版本中，这些参数字符串以纯文本形式存储在浏览器缓存中，因此不安全。  
  
## <a name="see-also"></a>请参阅  
 [新增功能&#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [SQL Server 2014 中的 SQL Server Reporting Services 的行为更改](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [SQL Server 2014 的 SQL Server Reporting Services 中弃用的功能](deprecated-features-in-sql-server-reporting-services-ssrs.md)  
  
  
