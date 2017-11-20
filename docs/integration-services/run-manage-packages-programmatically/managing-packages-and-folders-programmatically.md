---
title: "以编程方式管理包和文件夹 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a40acf3a586c74119d948291fd179f78833cb37a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="managing-packages-and-folders-programmatically"></a>以编程方式管理包和文件夹
<a name="top"></a>当您使用以编程方式[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]包，你可能想要确定是否将存在单个包或文件夹，或管理在其中存储包的文件夹。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空间的 <xref:Microsoft.SqlServer.Dts.Runtime> 类提供了多种满足这些要求的方法。    
    
##  <a name="exists"></a>确定是否存在包或文件夹    
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
    
 [返回页首](#top)    
    
##  <a name="managing"></a>管理包和文件夹    
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空间的 <xref:Microsoft.SqlServer.Dts.Runtime> 类提供其他用于管理包和存储包的文件夹的方法。    
    
###  <a name="managing_rempkg"></a>删除程序包    
 若要以编程方式删除已保存的包，请调用以下方法之一：    
    
|存储位置|调用的方法|    
|----------------------|--------------------|    
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [返回页首](#top)    
    
###  <a name="managing_create"></a>创建文件夹    
 若要以编程方式创建存储文件夹，请调用以下方法之一：    
    
|存储位置|调用的方法|    
|----------------------|--------------------|    
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [返回页首](#top)    
    
###  <a name="managing_remfldr"></a>删除文件夹    
 若要以编程方式删除存储文件夹，请调用以下方法之一：    
    
|存储位置|调用的方法|    
|----------------------|--------------------|    
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [返回页首](#top)    
    
###  <a name="managing_rename"></a>重命名文件夹    
 若要以编程方式重命名存储文件夹，请调用以下方法之一：    
    
|存储位置|调用的方法|    
|----------------------|--------------------|    
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [返回页首](#top)    
    
## <a name="see-also"></a>另请参阅    
 [包管理 &#40;SSIS 服务 &#41;](../../integration-services/service/package-management-ssis-service.md)     
 [以编程方式枚举可用的包](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  

