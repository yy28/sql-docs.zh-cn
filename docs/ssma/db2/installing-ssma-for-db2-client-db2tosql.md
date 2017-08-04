---
title: "安装适用于 DB2 客户端 (DB2ToSQL) SSMA |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4e003c72b6fea28c3048384701f3dc8839faacce
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>安装适用于 DB2 客户端 (DB2ToSQL) SSMA
SSMA 客户端包含的程序文件的执行以下任务：  
  
-   连接到 DB2 数据库。  
  
-   连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   转换到 DB2 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法。  
  
-   将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
本主题提供安装先决条件以及安装 SSMA 的说明。  
  
## <a name="prerequisites"></a>必要條件  
SSMA 用于处理上 z/OS 版本 9.0 和 10.0 的 DB2 或 LUW 9.8 和 10.1 或更高版本上的 DB2 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年。  
  
在安装 SSMA 之前，请确保计算机满足以下要求：  
  
-   Windows 7 或更高版本，或 Windows Server 2008 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本 4.0 或更高版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]上提供了版本 4.0[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]产品媒体。 你还可以获取从[.NET Framework 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Microsoft OLEDB Provider for DB2 版本 5 或更高版本，然后连接到你想要迁移 DB2 数据库。  
  
-   访问和承载的目标实例的计算机上的权限不足[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或你将数据库对象和数据迁移的 Azure SQL DB。 有关详细信息，请参阅[连接到 SQL Server &#40; DB2eToSQL &#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)。  
  
-   4 GB RAM 建议。  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Microsoft OLEDB Provider for DB2  
若要下载 OLEDB provider for DB2 版本 5.0，请转到[Microsoft® SQL Server® 2014年功能包](http://www.microsoft.com/download/details.aspx?id=42295)。  
  
SSMA 是一个 Web 下载。 若要下载最新版本，请参阅[SQL Server Migration Assistant 下载页](http://aka.ms/ssmafordb2)。  
  
下载最新版本之后，你必须提取中的安装文件，然后才能安装 SSMA。  
  
**若要安装 SSMA 客户端**  
  
1.  双击 SSMA for DB2  *n* 。Install.exe，其中 *n* 为内部版本号。  
  
2.  在欢迎页上，单击**下一步**。  
  
    如果还没有安装必备组件，将显示一条消息，该值指示你必须首先安装所需的组件。 请确保已安装所有必备条件，然后重新运行安装程序。  
  
3.  阅读最终用户许可协议。 如果同意，请选中**我接受许可协议中的条款**，然后单击**下一步**。  
  
4.  在选择安装类型页上，单击**典型**。  
  
5.  单击 **“安装”**。  
  
> [!IMPORTANT]  
> 1.  请在安装新版本之前 for DB2 卸载所有以前的 SSMA 版本。  
  
默认安装位置为 C:\Program Files\Microsoft SQL Server Migration Assistant for DB2。  
  
## <a name="see-also"></a>另请参阅  
[在 SQL Server &#40; DB2ToSQL &#41; 上安装 SSMA 组件](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[将 DB2 数据库迁移到 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

