---
title: 安装 SSMA for MySQL 客户端 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: de32849e59f0244baa62a5e7784b3ec2f26aacac
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393598"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>安装 SSMA for MySQL 客户端 (MySQLToSQL)
SSMA for MySQL 客户端包含的程序文件的执行以下任务：  
  
-   连接到 MySQL 数据库。  
  
-   连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
-   将转换为的 MySQL 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象。  
  
-   将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
-   将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
本主题提供的安装先决条件和安装 SSMA for MySQL 客户端的说明。  
  
## <a name="prerequisites"></a>必要條件  
适用于 MySQL 的 SSMA 设计用于 MySQL 4.1 或更高版本和所有版本的 SQL Server 2005、 SQL Server 2008、 SQL Server 2012 中，SQL Server 2014，SQL Server 2016、 SQL Server 2017 和 Azure SQL DB。  
  
安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本 4.0 或更高版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本 4.0 是 SQL Server 产品介质上的可用。 你还可以获取从[.NET Framework 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   MySQL ODBC 5.1 驱动程序和连接到你想要迁移的 MySQL 数据库。 可以从 MySQL 网站上安装 MySQL。 有关连接性的信息，请参阅[连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   访问和承载 SQL Server，你将数据库对象和数据迁移的目标实例的计算机上的权限不足。 有关详细信息，请参阅[连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   对于 SQL Azure 项目中，访问和足够的权限访问的实例将迁移你的 Azure SQL DB 的数据库对象和数据。 有关详细信息，请参阅[连接到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)。  
  
-   4 GB RAM 建议。  
  
## <a name="installing-ssma-for-mysql-client"></a>安装 SSMA for MySQL 客户端  
SSMA 是一个 Web 下载。 若要下载最新版本，请参阅[SQL Server Migration Assistant 下载页](http://aka.ms/ssmaformysql)。  
  
下载最新版本后，您必须提取安装文件，然后才能安装 SSMA。  
  
**安装 SSMA 客户端**  
  
1.  双击用于 MySQL 的 SSMA *n*。Install.exe，其中*n*是生成号。  
  
2.  在欢迎页上，单击**下一步**。  
  
    如果还没有安装必备组件，则会显示一条消息，指示您必须首先安装所需的组件。 请确保已重新运行安装程序前安装所有必备组件。  
  
3.  阅读最终用户许可协议。 如果同意，请选择**我接受许可协议中条款**，然后单击**下一步**。  
  
4.  在选择安装类型页上单击**典型**。  
  
5.  单击 **“安装”**。  
  
> [!IMPORTANT]  
> 1.  请安装新版本之前卸载 for MySQL 的所有早期版本的 SSMA。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server Migration Assistant for MySQL。  
  
在 64 位版本的 Windows 计算机产品安装在 C:\Microsoft SQL Server Migration Assistant for MySQL。  
  
## <a name="see-also"></a>请参阅  
[迁移 MySQL 数据库移到 SQL Server-Azure SQL 数据库&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
