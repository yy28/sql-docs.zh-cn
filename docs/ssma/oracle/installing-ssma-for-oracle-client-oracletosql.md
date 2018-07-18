---
title: 安装适用于 Oracle 客户端 (OracleToSQL) SSMA |Microsoft 文档
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: bacc738ab794c3ce215c000ee2c6980c09722b46
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777523"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>安装适用于 Oracle 客户端 (OracleToSQL) SSMA
SSMA 客户端包含的程序文件的执行以下任务：  
  
-   连接到 Oracle 数据库。  
  
-   连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   转换到的 Oracle 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法。  
  
-   将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
本主题提供安装先决条件以及安装 SSMA 的说明。  
  
## <a name="prerequisites"></a>必要條件  
SSMA 旨在与 Oracle 9 或更高版本和所有版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
在安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本，或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本 4.0 或更高版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]上提供了版本 4.0[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]产品媒体。 你还可以获取从[.NET Framework 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Oracle 客户端 9.0 或更高版本，并连接到你想要迁移的 Oracle 数据库。 Oracle 客户端版本必须与，相同的版本或更高版本比 Oracle 数据库版本。  
  
    你可以从 Oracle 产品媒体或从 Oracle 网站上安装 Oracle 客户端。 有关连接的信息，请参阅[连接到 Oracle 数据库&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
-   访问和承载的目标实例的计算机上的权限不足[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或你将数据库对象和数据迁移的 Azure SQL DB。 有关详细信息，请参阅[连接到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)。  
  
-   4 GB RAM 建议。  
  
## <a name="installing-the-ssma-for-oracle-client"></a>安装适用于 Oracle 客户端 SSMA  
SSMA 是一个 Web 下载。 若要下载最新版本，请参阅[SQL Server Migration Assistant 下载页](http://aka.ms/ssmafororacle)。  
  
下载最新版本之后，你必须提取中的安装文件，然后才能安装 SSMA。  
  
**若要安装 SSMA 客户端**  
  
1.  对于 Oracle 双击 SSMA *n*。Install.exe，其中*n*为内部版本号。  
  
2.  在欢迎页上，单击**下一步**。  
  
    如果还没有安装必备组件，将显示一条消息，该值指示你必须首先安装所需的组件。 请确保已安装所有必备条件，然后重新运行安装程序。  
  
3.  阅读最终用户许可协议。 如果同意，请选中**我接受许可协议中的条款**，然后单击**下一步**。  
  
4.  在选择安装类型页上，单击**典型**。  
  
5.  单击 **“安装”**。  
  
> [!IMPORTANT]  
> 1.  请在安装新版本之前卸载所有以前的 SSMA for Oracle 版本。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server Migration Assistant for Oracle。  
  
除了 SSMA 程序文件，你还必须安装 Oracle 扩展包的 SSMA 上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关详细信息，请参阅[SQL 服务器上安装 SSMA 组件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>请参阅  
[在 SQL Server 上安装 SSMA 组件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[迁移的 Oracle 数据库移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
