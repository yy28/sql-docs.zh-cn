---
title: 安装 SSMA for MySQL Client （MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9dcdeaff1c4782453a9fd57cc709e17ad3200d28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086817"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>安装 SSMA for MySQL 客户端 (MySQLToSQL)
SSMA for MySQL 客户端包含执行以下任务的程序文件：  
  
-   连接到 MySQL 数据库。  
  
-   连接到实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
-   将 MySQL 数据库对象转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象。  
  
-   将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
-   将数据迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到或 SQL Azure。  
  
本主题提供安装 SSMA for MySQL 客户端的安装先决条件和说明。  
  
## <a name="prerequisites"></a>必备条件  
SSMA for MySQL 旨在与 MySQL 4.1 或更高版本以及所有版本的 SQL Server 2005、SQL Server 2008、SQL Server 2012、SQL Server 2014、SQL Server 2016、SQL Server 2017 和 Azure SQL DB 配合使用。  
  
安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本，或 Windows Server 2008 或更高版本。  
  
-   
  [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]版本4.0 或更高[!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本4.0 在 SQL Server 产品媒体上提供。 你还可以从[.NET Framework 开发人员中心](https://go.microsoft.com/fwlink/?LinkId=48882)获取它。  
  
-   MySQL ODBC 5.1 驱动程序和与要迁移的 MySQL 数据库的连接。 你可以从 MySQL 网站安装 MySQL。 有关连接的详细信息，请参阅[连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   在承载 SQL Server 的目标实例的计算机上访问和足够的权限，你将在该计算机上迁移数据库对象和数据。 有关详细信息，请参阅[连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   如果是 SQL Azure 项目，则可以访问 Azure SQL 数据库实例，并对其拥有足够的权限，你将在其中迁移数据库对象和数据。 有关详细信息，请参阅[连接到 AZURE SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)。  
  
-   建议使用 4 GB RAM。  
  
## <a name="installing-ssma-for-mysql-client"></a>安装 SSMA for MySQL 客户端  
SSMA 是一款可以从 Web 下载的工具。 若要下载最新版本，请参阅[SQL Server 迁移助手下载 "页](https://aka.ms/ssmaformysql)。  
  
下载最新版本后，必须先提取安装文件，然后才能安装 SSMA。  
  
**安装 SSMA 客户端**  
  
1.  双击 "SSMA for MySQL *n*"。Setup.exe，其中*n*是生成号。  
  
2.  在“欢迎”页面上，单击“**下一步**”。  
  
    如果未安装必备组件，则将显示一条消息，指示必须首先安装所需的组件。 再次运行安装程序之前，请确保已安装所有必备组件。  
  
3.  阅读最终用户许可协议。 如果同意，请选择 **"我接受许可协议中的条款**"，然后单击 "**下一步**"。  
  
4.  在 "选择安装类型" 页上，单击 "**典型**"。  
  
5.  单击 **“安装”**。  
  
> [!IMPORTANT]  
> 1.  安装新版本之前，请卸载所有以前版本的 SSMA for MySQL。  
  
默认安装位置为 MySQL 的 C:\Program Files\Microsoft SQL Server 迁移助手。  
  
在64位 Windows 计算机上，该产品安装在 C:\Microsoft SQL Server 迁移助手 for MySQL 中。  
  
## <a name="see-also"></a>另请参阅  
[将 MySQL 数据库迁移到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
