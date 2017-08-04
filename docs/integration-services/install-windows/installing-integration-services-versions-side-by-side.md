---
title: "安装 Integration Services 版本并行 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d642d8d9d732a51c210e5d83cecf2b090ac2f426
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="installing-integration-services-versions-side-by-side"></a>并行安装 Integration Services 版本
  你可以安装   
      [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Integration Services (SSIS) 的并行与早期版本的 SSIS。 本主题介绍并行安装的一些限制。  
  
## <a name="designing-and-maintaining-packages"></a>设计和维护包  
 若要设计和维护面向 SQL Server 2016、SQL Server 2014 或 SQL Server 2012 的包，请使用 SQL Server Data Tools (SSDT) for Visual Studio 2015。 要获取 SSDT，请参阅 [下载最新的 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)。  
  
 在 Integration Services 项目属性页中，在“配置属性”  的“常规” 选项卡上，选择“TargetServerVersion”  属性，然后选择 SQL Server 2016、SQL Server 2014 或 SQL Server 2012。  
  
|SQL Server 的目标版本|SSIS 包的开发环境|  
|----------------------------------|-----------------------------------------------|  
|2016|适用于 Visual Studio 2015 的 SQL Server Data Tools|  
|2014|适用于 Visual Studio 2015 的 SQL Server Data Tools<br /><br /> 或<br /><br /> SQL Server Data Tools - Business Intelligence for Visual Studio 2013|  
|2012|适用于 Visual Studio 2015 的 SQL Server Data Tools<br /><br /> 或<br /><br /> SQL Server Data Tools - Business Intelligence for Visual Studio 2012|  
|2008|来自 SQL Server 2008 的 Business Intelligence Development Studio|  
  
 当将现有包添加到现有项目时，包将转换为项目所面向的格式。  
  
## <a name="running-packages"></a>运行包  
 你可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的 **dtexec** 实用程序或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理来运行早期版本的开发工具所创建的 Integration Services 包。 当这些 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 工具加载早期版本的开发工具开发的包时，该工具暂时将内存中的包转换为 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 使用的包格式。 如果包存在问题导致无法转换成功，则在这些问题解决之前， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 工具将无法运行该包。 有关详细信息，请参阅 [升级 Integration Services 包](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
  
