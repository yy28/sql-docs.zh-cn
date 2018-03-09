---
title: "SSMA 安装 MySQL 客户端 (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
caps.latest.revision: 
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ef326d0a41ceb09a412216c8dd36574b10f694b
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>SSMA 安装 MySQL 客户端 (MySQLToSQL)
SSMA for MySQL 客户端包含的程序文件的执行以下任务：  
  
-   连接到 MySQL 数据库。  
  
-   连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
-   将转换为的 MySQL 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 对象。  
  
-   将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
-   将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
本主题提供安装先决条件以及为 MySQL 客户端安装 SSMA 的说明。  
  
## <a name="prerequisites"></a>必要條件  
有关 MySQL 的 SSMA 旨在使用 MySQL 4.1 或更高版本和所有版本的 SQL Server 2005、 SQL Server 2008、 SQL Server 2012、 SQL Server 2014、 SQL Server 2016、 SQL Server 2017 和 Azure SQL DB。  
  
在安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本，或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本 4.0 或更高版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]上 SQL Server 产品媒体中提供了版本 4.0。 你还可以获取从[.NET Framework 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   MySQL ODBC 5.1 驱动程序并连接到你想要迁移的 MySQL 数据库。 你可以将 MySQL 安装从 MySQL 网站。 有关连接的信息，请参阅[连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   访问和承载 SQL Server，你将数据库对象和数据迁移的目标实例的计算机上的权限不足。 有关详细信息，请参阅[连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   发生 SQL Azure 项目中，访问和足够的权限访问的实例将迁移你的 Azure SQL DB 数据库对象和数据。 有关详细信息，请参阅[连接到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)。  
  
-   4 GB RAM 建议。  
  
## <a name="installing-ssma-for-mysql-client"></a>安装 MySQL 客户端的 SSMA  
SSMA 是一个 Web 下载。 若要下载最新版本，请参阅[SQL Server Migration Assistant 下载页](http://aka.ms/ssmaformysql)。  
  
下载最新版本之后，你必须提取安装文件，然后才能安装 SSMA。  
  
**若要安装 SSMA 客户端**  
  
1.  有关 MySQL，请双击 SSMA *n*。Install.exe，其中*n*为内部版本号。  
  
2.  在欢迎页上，单击**下一步**。  
  
    如果你没有安装的先决条件，一条消息将出现，指明你必须首先安装所需的组件。 请确保已在再次运行安装程序之前安装所有必备组件。  
  
3.  阅读最终用户许可协议。 如果同意，请选中**我接受许可协议中的条款**，然后单击**下一步**。  
  
4.  在选择安装类型页上，单击**典型**。  
  
5.  单击 **“安装”**。  
  
> [!IMPORTANT]  
> 1.  请在安装新版本之前 mysql 卸载所有以前的 SSMA 版本。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server Migration Assistant for MySQL。  
  
在 64 位 Windows 计算机上的产品中 C:\Microsoft SQL Server Migration Assistant 安装为 MySQL。  
  
## <a name="see-also"></a>另请参阅  
[迁移的 MySQL 数据库移到 SQL Server 的 Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
