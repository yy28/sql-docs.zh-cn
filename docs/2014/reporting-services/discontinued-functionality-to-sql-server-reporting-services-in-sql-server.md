---
title: 停用的功能
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 8cdec8ed3fbdd539b0c630af2a298ebf9807d6a7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755757"
---
# <a name="discontinued-functionality-in-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS) 中停止使用的功能

  此主题介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中不再可用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。 此处不包括关于停止支持某些版本的操作系统或 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Services (IIS) 的声明。 有关系统先决条件的详细信息，请参阅[安装 SQL Server 2014 的硬件和软件要求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
 本主题内容：  
  
- [SQL Server 2014 Reporting Services 停用的功能](#bkmk_sql14)  
  
- [SQL Server 2012 Reporting Services 中停止使用的功能](#bkmk_rc0)  
  
- [SQL Server 2008 R2 Reporting Services 中停止使用的功能](#bkmk_kj)  
  
##  <a name="sssql14-reporting-services-discontinued-functionality"></a><a name="bkmk_sql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Reporting Services 中止的功能

 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中没有已停止使用的 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]功能。  
  
##  <a name="sssql11-reporting-services-discontinued-functionality"></a><a name="bkmk_rc0"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]Reporting Services 中止的功能

 本节介绍 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中停止使用的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]功能。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中没有已停止使用的 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]功能。  
  
##  <a name="sql-server-2008-r2-reporting-services-discontinued-functionality"></a><a name="bkmk_kj"></a>SQL Server 2008 R2 Reporting Services 废止功能

 本部分介绍中的停止使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 。  
  
> [!NOTE]  
> 因为 SQL Server 2008 R2 是 SQL Server 2008 的次版本升级，所以，我们建议您也查看 SQL Server 2008 部分的内容。
  
### <a name="64-bit-platform-support"></a>64 位平台支持

 从 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 开始，[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 组件不再支持运行 Windows Server 2003 或 Windows Server 2003 R2 的基于 Itanium 的服务器。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]继续支持其他64位操作系统，包括适用于基于 Itanium 的系统的 Windows Server 2008 和基于 Itanium 的系统的 Windows Server 2008 R2。 若要在 Windows Server 2003 或 Windows Server 2003 R2 的基于 Itanium 的系统版本上从具有 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 安装升级到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，您必须首先升级操作系统。  
  
### <a name="data-source-credentials-in-url-access"></a>URL 访问中的数据源凭据

 URL 访问参数字符串*dsu：值 = 值*和*dsp：值 = 值*现在已停止使用。 在早期版本中，这些参数字符串以纯文本形式存储在浏览器缓存中，因此不安全。  
  
## <a name="next-steps"></a>后续步骤

 - [新增功能 &#40;Reporting Services&#41;](what-s-new-reporting-services.md)
 - [SQL Server 2014 中 SQL Server Reporting Services 的行为更改](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)
 - [SQL Server 2014 的 SQL Server Reporting Services 中不推荐使用的功能](deprecated-features-in-sql-server-reporting-services-ssrs.md)