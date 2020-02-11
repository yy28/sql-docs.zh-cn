---
title: 为 Oracle 客户端安装 SSMA （OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: fc295e108357040617bf6bdaa1af61fada2c97ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68259683"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>安装 SSMA for Oracle 客户端 (OracleToSQL)
SSMA 客户端由执行以下任务的程序文件组成：  
  
-   连接到 Oracle 数据库。  
  
-   连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   将 Oracle 数据库对象转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为语法。  
  
-   将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。  
  
-   将数据迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到。  
  
本主题提供安装 SSMA 的安装先决条件和说明。  
  
## <a name="prerequisites"></a>必备条件  
SSMA 旨在用于 Oracle 9 或更高版本以及的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所有版本。  
  
安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本，或 Windows Server 2008 或更高版本。  
  
-   
  [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]版本4.0 或更高[!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本4.0 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]产品介质上可用。 你还可以从[.NET Framework 开发人员中心](https://go.microsoft.com/fwlink/?LinkId=48882)获取它。  
  
-   Oracle 客户端9.0 或更高版本，以及与要迁移的 Oracle 数据库的连接。 Oracle 客户端版本的版本必须与 Oracle 数据库版本的版本相同，或更高版本。  
  
    可以从 Oracle 产品媒体或 Oracle 网站安装 Oracle 客户端。 有关连接的详细信息，请参阅[连接到 Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
-   在承载[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 AZURE SQL 数据库的目标实例的计算机上访问和足够的权限，你将在该计算机上迁移数据库对象和数据。 有关详细信息，请参阅[连接到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)。  
  
-   建议使用 4 GB RAM。  
  
## <a name="installing-the-ssma-for-oracle-client"></a>安装 SSMA for Oracle 客户端  
SSMA 是一款可以从 Web 下载的工具。 若要下载最新版本，请参阅[SQL Server 迁移助手下载 "页](https://aka.ms/ssmafororacle)。  
  
下载最新版本后，必须从中提取安装文件，然后才能安装 SSMA。  
  
**安装 SSMA 客户端**  
  
1.  双击 "SSMA for Oracle *n*"。Setup.exe，其中*n*是生成号。  
  
2.  在“欢迎”页面上，单击“**下一步**”。  
  
    如果未安装必备组件，则会出现一条消息，指示必须首先安装所需的组件。 请确保已安装所有必备组件，然后再次运行安装程序。  
  
3.  阅读最终用户许可协议。 如果同意，请选择 **"我接受许可协议中的条款**"，然后单击 "**下一步**"。  
  
4.  在 "选择安装类型" 页上，单击 "**典型**"。  
  
5.  单击 **“安装”**。  
  
> [!IMPORTANT]  
> 1.  安装新版本之前，请卸载所有以前版本的 SSMA for Oracle。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server 迁移助手。  
  
除了 SSMA 程序文件之外，还必须在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装 SSMA for Oracle 扩展包。 有关详细信息，请参阅[SQL Server &#40;OracleToSQL&#41;上安装 SSMA 组件](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>另请参阅  
[在 SQL Server 上安装 SSMA 组件 &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[将 Oracle 数据库迁移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
