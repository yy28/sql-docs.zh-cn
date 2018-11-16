---
title: 安装 SSMA for Sybase 客户端 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6cca10f2a54a70e91e46bb8b98e9799885b5f175
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51671717"
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>安装 SSMA for Sybase 客户端 (SybaseToSQL)
SSMA 客户端包含的程序文件的用于连接到 Sybase Adaptive Server Enterprise (ASE) 数据库服务器和实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，将转换到 ASE 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 语法，加载将对象插入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，然后将数据迁移到和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQLDB。  
  
本主题提供安装先决条件和安装 SSMA 的说明。  
  
## <a name="prerequisites"></a>必要條件  
SSMA 设计用于 ASE 11.9.2 或更高版本和所有版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 版本 4.0 或更高版本。 .NET Framework 4.0 版位于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]产品媒体。 你还可以获取从[.NET Framework 开发人员中心](https://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Sybase OLEDB/ADO.Net/ODBC 提供程序和连接到 Sybase ASE 数据库服务器包含你想要迁移的数据库中。 您可以从 Sybase ASE 产品媒体中安装提供程序。 有关连接性的信息，请参阅[连接到 Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。  
  
-   访问和承载的目标实例的计算机上的权限不足[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或要将数据库对象和数据迁移的 Azure SQL DB。 有关详细信息，请参阅[连接到 SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)/[连接到 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)。  
  
-   4 GB RAM 建议。  
  
## <a name="installing-the-ssma-for-sybase-client"></a>安装 SSMA for Sybase 客户端  
SSMA 是一个 Web 下载。 若要下载最新版本，请参阅[SQL Server Migration Assistant 下载页](https://aka.ms/ssmaforsybase)。  
  
下载最新版本后，您必须提取中的安装文件，然后才能安装 SSMA。  
  
**安装 SSMA 客户端**  
  
1.  双击 SSMA for Sybase *n*。Install.exe，其中*n*是生成号。  
  
2.  在欢迎页上，单击**下一步**。  
  
    如果还没有安装必备组件，将显示一条消息，指示您必须首先安装所需的组件。 请确保已安装所有必备组件，然后重新运行安装程序。  
  
3.  阅读最终用户许可协议。 如果同意，请选择**我接受许可协议中条款**，然后单击**下一步**。  
  
4.  在选择安装类型页上单击**典型**。  
  
5.  单击 **“安装”**。  
  
> [!IMPORTANT]  
> 1.  请安装新版本之前卸载 for Sybase 的所有早期版本的 SSMA。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase。  
  
除了 SSMA 程序文件，您还必须安装 SSMA for Sybase 扩展包上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[SQL Server 上安装 SSMA 组件&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)。  
  
## <a name="see-also"></a>请参阅  
[SQL Server 上安装 SSMA 组件&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
