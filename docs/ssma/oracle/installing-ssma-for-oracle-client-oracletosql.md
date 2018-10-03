---
title: 安装 SSMA for Oracle 客户端 (OracleToSQL) |Microsoft Docs
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
manager: v-thobro
ms.openlocfilehash: 72df6a9da82e421dfb921501c110d363aa54a8f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781552"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>安装 SSMA for Oracle 客户端 (OracleToSQL)
SSMA 客户端包含的程序文件的执行以下任务：  
  
-   连接到 Oracle 数据库。  
  
-   连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   转换到的 Oracle 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法。  
  
-   将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
本主题提供安装先决条件和安装 SSMA 的说明。  
  
## <a name="prerequisites"></a>必要條件  
SSMA 设计用于 Oracle 9 或更高版本和所有版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本 4.0 或更高版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版位于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]产品媒体。 你还可以获取从[.NET Framework 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Oracle 客户端 9.0 或更高版本，并与你想要迁移的 Oracle 数据库的连接。 Oracle 客户端版本必须是版本相同或比 Oracle 数据库版本更高版本。  
  
    您可以从 Oracle 产品媒体或从 Oracle 网站上安装 Oracle 客户端。 有关连接性的信息，请参阅[连接到 Oracle 数据库&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
-   访问和承载的目标实例的计算机上的权限不足[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或要将数据库对象和数据迁移的 Azure SQL DB。 有关详细信息，请参阅[连接到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)。  
  
-   4 GB RAM 建议。  
  
## <a name="installing-the-ssma-for-oracle-client"></a>安装 SSMA for Oracle 客户端  
SSMA 是一个 Web 下载。 若要下载最新版本，请参阅[SQL Server Migration Assistant 下载页](http://aka.ms/ssmafororacle)。  
  
下载最新版本后，您必须提取中的安装文件，然后才能安装 SSMA。  
  
**安装 SSMA 客户端**  
  
1.  双击用于 Oracle 的 SSMA *n*。Install.exe，其中*n*是生成号。  
  
2.  在欢迎页上，单击**下一步**。  
  
    如果还没有安装必备组件，将显示一条消息，指示您必须首先安装所需的组件。 请确保已安装所有必备组件，然后重新运行安装程序。  
  
3.  阅读最终用户许可协议。 如果同意，请选择**我接受许可协议中条款**，然后单击**下一步**。  
  
4.  在选择安装类型页上单击**典型**。  
  
5.  单击 **“安装”**。  
  
> [!IMPORTANT]  
> 1.  请安装新版本之前卸载所有以前版本的适用于 Oracle 的 SSMA。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server Migration Assistant for Oracle。  
  
除了 SSMA 程序文件，您还必须安装 SSMA for Oracle 扩展包上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[SQL Server 上安装 SSMA 组件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>请参阅  
[SQL Server 上安装 SSMA 组件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[迁移的 Oracle 数据库移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
