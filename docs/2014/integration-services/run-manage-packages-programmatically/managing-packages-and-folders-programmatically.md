---
title: 以编程方式管理包和文件夹 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 08eb3bbd5ea03b7744daa8507164576c0700f0f8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124599"
---
# <a name="managing-packages-and-folders-programmatically"></a>以编程方式管理包和文件夹
  以编程方式使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包时，您可能希望确定个别包或文件夹是否存在，或管理用于存储包的文件夹。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空间的 <xref:Microsoft.SqlServer.Dts.Runtime> 类提供了多种满足这些要求的方法。  
  
##  <a name="exists"></a>确定包或文件夹是否存在  
 若要以编程方式确定已保存的包是否存在，请先调用以下方法之一，然后尝试加载和运行该包：  
  
|存储位置|调用的方法|  
|----------------------|--------------------|  
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|  
  
 若要以编程方式确定文件夹是否存在，请先调用以下方法之一，然后尝试列出其中存储的包：  
  
|存储位置|调用的方法|  
|----------------------|--------------------|  
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|  
  

  
##  <a name="managing"></a>管理包和文件夹  
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空间的 <xref:Microsoft.SqlServer.Dts.Runtime> 类提供其他用于管理包和存储包的文件夹的方法。  
  
###  <a name="managing_rempkg"></a>删除包  
 若要以编程方式删除已保存的包，请调用以下方法之一：  
  
|存储位置|调用的方法|  
|----------------------|--------------------|  
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|  
  

  
###  <a name="managing_create"></a>创建文件夹  
 若要以编程方式创建存储文件夹，请调用以下方法之一：  
  
|存储位置|调用的方法|  
|----------------------|--------------------|  
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|  
  

  
###  <a name="managing_remfldr"></a>删除文件夹  
 若要以编程方式删除存储文件夹，请调用以下方法之一：  
  
|存储位置|调用的方法|  
|----------------------|--------------------|  
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|  
  
  
  
###  <a name="managing_rename"></a>重命名文件夹  
 若要以编程方式重命名存储文件夹，请调用以下方法之一：  
  
|存储位置|调用的方法|  
|----------------------|--------------------|  
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|  
  

  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新集成服务** <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的集成服务页](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [包管理（SSIS 服务）](../service/package-management-ssis-service.md)   
 [以编程方式枚举可用的包](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  