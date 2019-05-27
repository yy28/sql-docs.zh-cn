---
title: 查看 Integration Services 包在 SQL Server Management Studio （SSIS 服务） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- viewing packages
- connections [Integration Services], packages
ms.assetid: 783e653c-0f1f-45ed-b3ef-5ba07b019f27
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0d8196a46437975a2b8e00bb2fbe8d183540025c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66054611"
---
# <a name="view-integration-services-packages-in-sql-server-management-studio-ssis-service"></a>在 SQL Server Management Studio 中查看 Integration Services 包（SSIS 服务）
    
> [!IMPORTANT]  
>  本主题论述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支持该服务以便与 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的早期版本向后兼容。 从 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]开始，您可以在 Integration Services 服务器上管理诸如包之类的对象。  
  
 本过程介绍在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中如何连接到 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 并查看 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务所管理的包的列表。  
  
### <a name="to-connect-to-integration-services"></a>连接到 Integration Services  
  
1.  单击 **“开始”**，依次指向 **“所有程序”** 和 **Microsoft SQL Server**，然后单击 **SQL Server Management Studio**。  
  
2.  在 **“连接到服务器”** 对话框中，在 **“服务器类型”** 列表中选择 **Integration Services** ，在 **“服务器名称”** 框中提供服务器名称，然后单击 **“连接”**。  
  
    > [!IMPORTANT]  
    >  如果无法连接到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]，则 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务可能未运行。 若要了解该服务的状态，请单击 **“开始”**，依次指向 **“所有程序”**、 **Microsoft SQL Server**和 **“配置工具”**，再单击 **“SQL Server 配置管理器”**。 在左窗格中，单击 **“SQL Server 服务”**。 在右窗格中，查找 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务。 如果该服务尚未运行，请启动该服务。  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 。 默认情况下，会打开对象资源管理器窗口并定位在 SQL Server Management Studio 左下角。 如果对象资源管理器未打开，请单击 **“视图”** 菜单上的 **“对象资源管理器”** 。  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>查看 Integration Services 服务管理的包  
  
1.  在对象资源管理器中，展开“已存储的包”文件夹。  
  
2.  展开“已存储的包”子文件夹，以显示包。  
  
## <a name="see-also"></a>请参阅  
 [包管理（SSIS 服务）](service/package-management-ssis-service.md)   
 [使用 SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)  
  
  
