---
title: 以编程方式管理包和文件夹 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f38f79f90a1ec39a013efc4efd03a13f96e51a72
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65719119"
---
# <a name="managing-packages-and-folders-programmatically"></a>以编程方式管理包和文件夹

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


<a name="top"></a>以编程方式使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包时，你可能希望确定个别包或文件夹是否存在，或管理用于存储包的文件夹。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空间的 <xref:Microsoft.SqlServer.Dts.Runtime> 类提供了多种满足这些要求的方法。    
    
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
    
 [返回首页](#top)    
    
##  <a name="managing"></a>管理包和文件夹    
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空间的 <xref:Microsoft.SqlServer.Dts.Runtime> 类提供其他用于管理包和存储包的文件夹的方法。    
    
###  <a name="managing_rempkg"></a>删除包    
 若要以编程方式删除已保存的包，请调用以下方法之一：    
    
|存储位置|调用的方法|    
|----------------------|--------------------|    
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [返回首页](#top)    
    
###  <a name="managing_create"></a>创建文件夹    
 若要以编程方式创建存储文件夹，请调用以下方法之一：    
    
|存储位置|调用的方法|    
|----------------------|--------------------|    
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [返回首页](#top)    
    
###  <a name="managing_remfldr"></a>删除文件夹    
 若要以编程方式删除存储文件夹，请调用以下方法之一：    
    
|存储位置|调用的方法|    
|----------------------|--------------------|    
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [返回首页](#top)    
    
###  <a name="managing_rename"></a>重命名文件夹    
 若要以编程方式重命名存储文件夹，请调用以下方法之一：    
    
|存储位置|调用的方法|    
|----------------------|--------------------|    
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [返回首页](#top)    
    
## <a name="see-also"></a>另请参阅    
 [包管理（SSIS 服务）](../../integration-services/service/package-management-ssis-service.md)     
 [以编程方式枚举可用的包](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  
