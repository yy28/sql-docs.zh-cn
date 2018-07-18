---
title: Integration Services (SSIS) 服务器 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ea60bbdac3df4cd1130ba4afee83f882f138d33d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289393"
---
# <a name="integration-services-ssis-server"></a>Integration Services (SSIS) 服务器
  当您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中设计和测试包后，可将包含包的项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器是承载 `SSISDB` 数据库的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例。 该数据库存储以下对象：包、项目、参数、权限、服务器属性和操作历史记录。  
  
 `SSISDB` 数据库在您可以查询的公共视图中公开对象信息。 数据库还提供存储过程，您可以调用这些存储过程以管理该对象。  
  
 在您可以将项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器之前，需要创建 `SSISDB` 目录。  
  
 若要大致了解 SSISDB 目录功能，请参阅 [SSIS 目录](ssis-catalog.md)。  
  
## <a name="high-availability"></a>高可用性  
 像其他用户数据库，一样`SSISDB`database 数据库镜像和复制支持。 若要详细了解镜像和复制，请参阅[数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
 还可以通过利用 SSIS 和 AlwaysOn 可用性组，提供 SSISDB 及其内容的高可用性。 有关详细信息，请参阅 blogs.msdn.com 上 Matt Masson 的博客文章 [SSIS 与 AlwaysOn 一起使用](http://go.microsoft.com/fwlink/?LinkId=255873)。  
  
##  <a name="ssms"></a> SQL Server Management Studio 中的 Integration Services 服务器  
 在您连接到承载 `SSISDB` 数据库的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例时，您将在对象资源管理器中看到下列对象：  
  
-   **SSISDB 数据库**  
  
     `SSISDB`下显示数据库**数据库**节点在对象资源管理器。 您可以查询视图和调用存储过程，这些存储过程既管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器，也管理在该服务器上存储的对象。  
  
-   **Integration Services 目录**  
  
     在 **“Integration Services 目录”** 节点下，有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目和环境的文件夹。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [创建 SSIS 目录](../create-the-ssis-catalog.md)  
  
-   [查看 Integration Services 服务器上的包列表](view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [将项目部署到 Integration Services 服务器](../deploy-projects-to-integration-services-server.md)  
  
-   [使用 SQL Server Management Studio 在 SSIS 服务器上运行包](../run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="related-content"></a>相关内容  
 blogs.msdn.com 上的博客文章 [SSIS 与 AlwaysOn 一起使用](http://go.microsoft.com/fwlink/?LinkId=255873)。  
  
  
