---
title: "以编程方式管理包角色 （SSIS 服务） |Microsoft 文档"
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
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 7a7fb000389756caf0c2f2ea00cd0b80e75557d8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="managing-package-roles-programmatically-ssis-service"></a>以编程方式管理包角色（SSIS 服务）
  以编程方式使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包时，您可能希望确定哪些角色可以应用于包，或确定或设置应用于各个包的角色。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空间的 <xref:Microsoft.SqlServer.Dts.Runtime> 类提供了多种满足这些要求的方法。  
  
 角色仅适用于包存储在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**数据库。 有关包角色的详细信息，请参阅[Integration Services Roles &#40;SSIS 服务 &#41;](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 本主题中讨论的所有方法都需要对引用**Microsoft.SqlServer.ManagedDTS**程序集。 新项目中添加引用后，导入<xref:Microsoft.SqlServer.Dts.Runtime>命名空间使用**使用**或**导入**语句。  
  
> [!IMPORTANT]  
>  方法<xref:Microsoft.SqlServer.Dts.Runtime.Application>以便使用与 SSIS 包存储区中的类仅支持"。"，localhost 或服务器的本地服务器的名称。 不能使用“(local)”。  
  
## <a name="determining-which-roles-are-available"></a>确定哪些角色可用  
 若要确定哪些角色可用于存储在特定服务器上的包，可调用 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> 类的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 方法。  
  
## <a name="determining-which-roles-are-assigned"></a>确定哪些角色已分配  
 若要确定哪些角色已经分配给了特定包，可调用 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A> 方法。 若要将角色分配给包，可调用 <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A> 方法。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 角色 &#40;SSIS 服务 &#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  

