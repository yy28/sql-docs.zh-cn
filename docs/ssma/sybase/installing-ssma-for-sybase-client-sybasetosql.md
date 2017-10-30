---
title: "Sybase 客户端 (SybaseToSQL) 安装 SSMA |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c08bd0a90cc7f5820f2f1e9481f2c58c3b12f131
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>安装 SSMA for Sybase 客户端 (SybaseToSQL)
SSMA 客户端包含用于连接到 Sybase 自适应 Server Enterprise (ASE) 数据库服务器和实例的程序文件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，将转换到的 ASE 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 语法，将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，然后将数据迁移到和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQLDB。  
  
本主题提供安装先决条件以及安装 SSMA 的说明。  
  
## <a name="prerequisites"></a>必要條件  
SSMA 设计成可使用 ASE 11.9.2 或更高版本和所有版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
在安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本，或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 版本 4.0 或更高版本。 .NET Framework 版本 4.0 位于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]产品媒体。 你还可以获取从[.NET Framework 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Sybase OLEDB/ADO.Net/ODBC 提供程序和连接到包含你想要迁移的数据库的 Sybase ASE 数据库服务器。 你可以从 Sybase ASE 产品媒体中安装提供程序。 有关连接的信息，请参阅[连接到 Sybase ASE &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   访问和承载的目标实例的计算机上的权限不足[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或你将数据库对象和数据迁移的 Azure SQL DB。 有关详细信息，请参阅[连接到 SQL Server &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) /[连接到 Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
-   4 GB RAM 建议。  
  
## <a name="installing-the-ssma-for-sybase-client"></a>Sybase 客户端安装 SSMA  
SSMA 是一个 Web 下载。 若要下载最新版本，请参阅[SQL Server Migration Assistant 下载页](http://aka.ms/ssmaforsybase)。  
  
下载最新版本之后，你必须提取中的安装文件，然后才能安装 SSMA。  
  
**若要安装 SSMA 客户端**  
  
1.  双击用于 Sybase 的 SSMA  *n* 。Install.exe，其中 *n* 为内部版本号。  
  
2.  在欢迎页上，单击**下一步**。  
  
    如果还没有安装必备组件，将显示一条消息，该值指示你必须首先安装所需的组件。 请确保已安装所有必备条件，然后重新运行安装程序。  
  
3.  阅读最终用户许可协议。 如果同意，请选中**我接受许可协议中的条款**，然后单击**下一步**。  
  
4.  在选择安装类型页上，单击**典型**。  
  
5.  单击 **“安装”**。  
  
> [!IMPORTANT]  
> 1.  请在安装新版本之前用于 Sybase 卸载所有以前的 SSMA 版本。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server Migration Assistant 用于 Sybase。  
  
除了 SSMA 程序文件，你还必须安装 SSMA 用于 Sybase 扩展包在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关详细信息，请参阅[上 SQL Server &#40; 安装 SSMA 组件SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).  
  
## <a name="see-also"></a>另請參閱  
[在 SQL Server &#40; 上安装 SSMA 组件SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Sybase ASE 将数据库迁移到 SQL Server 的 Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

