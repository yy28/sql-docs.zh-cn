---
title: 为 Sybase 客户端安装 SSMA （SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8680685640b234e47f6e68d7fb802fc7e2f5d81c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029018"
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>安装 SSMA for Sybase 客户端 (SybaseToSQL)
SSMA 客户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]端包括用于连接到 Sybase 自适应服务器企业版（ASE）数据库服务器和实例或 AZURE sql 数据库的程序文件、将 ASE 数据库对象转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 azure sql db 语法、将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 azure sql 数据库，以及将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 azure SQLDB。  
  
本主题提供安装 SSMA 的安装先决条件和说明。  
  
## <a name="prerequisites"></a>先决条件  
SSMA 设计用于处理 ASE 11.9.2 或更高版本以及的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所有版本。  
  
安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本，或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 版本4.0 或更高版本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]产品介质上提供了 .NET Framework 版本4.0。 你还可以从[.NET Framework 开发人员中心](https://go.microsoft.com/fwlink/?LinkId=48882)获取它。  
  
-   Sybase OLEDB/ADO.Net/ODBC 提供程序和与 Sybase ASE 数据库服务器的连接，其中包含要迁移的数据库。 可以从 Sybase ASE 产品媒体安装提供程序。 有关连接的详细信息，请参阅[连接到 SYBASE ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。  
  
-   在承载[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 AZURE SQL 数据库的目标实例的计算机上访问和足够的权限，你将在该计算机上迁移数据库对象和数据。 有关详细信息，请参阅连接[到 SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) /[连接到 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)。  
  
-   建议使用 4 GB RAM。  
  
## <a name="installing-the-ssma-for-sybase-client"></a>为 Sybase 客户端安装 SSMA  
SSMA 是一款可以从 Web 下载的工具。 若要下载最新版本，请参阅[SQL Server 迁移助手下载 "页](https://aka.ms/ssmaforsybase)。  
  
下载最新版本后，必须从中提取安装文件，然后才能安装 SSMA。  
  
**安装 SSMA 客户端**  
  
1.  双击 "SSMA" 作为 "Sybase *n*"。Setup.exe，其中*n*是生成号。  
  
2.  在欢迎页上，单击 "**下一步**"。  
  
    如果未安装必备组件，则会出现一条消息，指示必须首先安装所需的组件。 请确保已安装所有必备组件，然后再次运行安装程序。  
  
3.  阅读最终用户许可协议。 如果同意，请选择 **"我接受许可协议中的条款**"，然后单击 "**下一步**"。  
  
4.  在 "选择安装类型" 页上，单击 "**典型**"。  
  
5.  单击“安装”  。  
  
> [!IMPORTANT]  
> 1.  请先卸载所有以前版本的 SSMA for Sybase，然后再安装新版本。  
  
默认安装位置为 Sybase 的 C:\Program Files\Microsoft SQL Server 迁移助手。  
  
除了 SSMA 程序文件之外，还必须在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装用于 Sybase 扩展包的 SSMA。 有关详细信息，请参阅[SQL Server &#40;SybaseToSQL&#41;上安装 SSMA 组件](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)。  
  
## <a name="see-also"></a>另请参阅  
[在 SQL Server 上安装 SSMA 组件 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
