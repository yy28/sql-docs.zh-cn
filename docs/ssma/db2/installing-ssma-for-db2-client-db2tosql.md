---
title: 安装 SSMA for DB2 客户端 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1d479c8f7de1c9d7463e57f37f9e8588c9bc68b6
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666496"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>安装 SSMA for DB2 客户端 (DB2ToSQL)
SSMA 客户端包含的程序文件的执行以下任务：  
  
-   连接到 DB2 数据库。  
  
-   连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   转换到 DB2 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法。  
  
-   将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
本主题提供安装先决条件和安装 SSMA 的说明。  
  
## <a name="prerequisites"></a>必要條件  
SSMA 用于处理 DB2 z/os 9.0 和 10.0 版本或 LUW 版本 9.8 和 10.1 或更高版本上的 DB2 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年。  
  
安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本 4.0 或更高版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版位于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]产品媒体。 你还可以获取从[.NET Framework 开发人员中心](https://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   为 DB2 版本 5 或更高版本，以及与你想要迁移的 DB2 数据库的 Microsoft OLEDB 访问接口。  
  
-   访问和承载的目标实例的计算机上的权限不足[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或要将数据库对象和数据迁移的 Azure SQL DB。 有关详细信息，请参阅[连接到 SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)。  
  
-   4 GB RAM 建议。  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Microsoft OLEDB Provider for DB2  
若要下载 OLEDB provider for DB2 版本 5.0，请转到[Microsoft® SQL Server® 2014年功能包](https://www.microsoft.com/download/details.aspx?id=42295)。  
  
SSMA 是一个 Web 下载。 若要下载最新版本，请参阅[SQL Server Migration Assistant 下载页](https://aka.ms/ssmafordb2)。  
  
下载最新版本后，您必须提取中的安装文件，然后才能安装 SSMA。  
  
**安装 SSMA 客户端**  
  
1.  双击 SSMA for DB2 *n*。Install.exe，其中*n*是生成号。  
  
2.  在欢迎页上，单击**下一步**。  
  
    如果还没有安装必备组件，将显示一条消息，指示您必须首先安装所需的组件。 请确保已安装所有必备组件，然后重新运行安装程序。  
  
3.  阅读最终用户许可协议。 如果同意，请选择**我接受许可协议中条款**，然后单击**下一步**。  
  
4.  在选择安装类型页上单击**典型**。  
  
5.  单击 **“安装”**。  
  
> [!IMPORTANT]  
> 1.  请安装新版本之前卸载 for DB2 的所有早期版本的 SSMA。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server Migration Assistant for DB2。  
  
## <a name="see-also"></a>请参阅  
[SQL Server 上安装 SSMA 组件&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[迁移的 DB2 数据库移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
