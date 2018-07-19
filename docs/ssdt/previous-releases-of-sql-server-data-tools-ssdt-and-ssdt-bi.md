---
title: 以前版本的 SQL Server Data Tools（SSDT 和 SSDT-BI）| Microsoft Docs
ms.custom: ''
ms.date: 07/02/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssdt
ms.reviewer: ''
ms.suite: sql
ms.technology: ssdt
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5d32e301-0f44-4916-b0db-76e8322c0ab7
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b638305cd88aacc1012ee9c23c94381f6746d709
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332387"
---
# <a name="previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi"></a>以前版本的 SQL Server Data Tools（SSDT 和 SSDT-BI）
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
SQL Server Data Tools (SSDT) 为生成 SQL Server 内容类型（关系数据库、Analysis Services 模型、Reporting Services 报表和 Integration Services 包）提供项目模板和设计图面。  
  
SSDT 可向后兼容，因此用户始终都可以使用[最新的 SSDT](download-sql-server-data-tools-ssdt.md) 来设计和部署在较早版本 SQL Server 上运行的数据库、模型、报表和包。  
  
> [!NOTE]  
> 以前，用于创建 SQL Server 内容类型的 Visual Studio shell 在各种不同的名称下发布，包括“SQL Server Data Tools” 、“SQL Server Data Tools-Business Intelligence” 和“Business Intelligence Development Studio” 。 以前的版本附带多组不同的项目模板。 若要在一个 SSDT 中同时获取全部项目模板，你需要 [最新版本](download-sql-server-data-tools-ssdt.md)。 否则，你可能需要安装多个以前的版本才可获取 SQL Server 中使用的全部模板。  每个 Visual Studio 版本只会安装一个 shell；安装另一个 SSDT 只会添加缺少的模板。  

## <a name="recent-downloads"></a>最近下载

所提供的最近的下载针对的是不太可能在[最新版本](download-sql-server-data-tools-ssdt.md)中遇到的问题。 

|SSDT 版本| Visual Studio 2017|
|:---|:---|
|15.7.0|[SSDT for VS2017 15.7.0](https://go.microsoft.com/fwlink/?LinkId=874716)|
|15.6.0|[SSDT for VS2017 15.6.0](https://go.microsoft.com/fwlink/?LinkId=871368)|
|15.5.2|[SSDT for VS2017 15.5.2](https://go.microsoft.com/fwlink/?LinkId=866452)|
<br>


|SSDT 版本| Visual Studio 2015|
|:---|:---|
|17.3|[SSDT for VS2015 17.3](https://go.microsoft.com/fwlink/?linkid=858660)| 
|16.5|[SSDT for VS2015 16.5](https://go.microsoft.com/fwlink/?LinkID=832313)|  
<br>

|SSDT 版本| Visual Studio 2013|
|:---|:---|
|16.5|[SSDT for VS2013 16.5](https://go.microsoft.com/fwlink/?LinkID=832308)|  
<br>


\* SSDT支持两个最新版本的 Visual Studio。 随着 Visual Studio 2017 的发布，将不再更新 SSDT for VS2013。 有关其他信息，请参阅[此 SSDT 团队博客文章](https://blogs.msdn.microsoft.com/ssdt/2017/03/10/sql-server-data-tools-17-0-rc-and-ssdt-in-vs2017/)的“常见问题解答”部分。

  
## <a name="links-to-download-pages"></a>下载页面的链接 
**SQL 关系数据库引擎**  
  
提供模板，用于为 RDBMS 和 Azure SQL 数据库生成关系数据库。 对于设计关系数据库，SSDT 与版本无关。 你可以将 Visual Studio 2012 或 2013 与任意版本的 SQL Server 数据库引擎或 Azure SQL 数据库一起使用。  
  
**数据库设计器**  
  
-   [下载 SSDT for Visual Studio 2013](https://msdn.microsoft.com/dn864412)  
  
-   [下载 SSDT for Visual Studio 2012](https://msdn.microsoft.com/jj650015)  
  
-   **适用于 Visual Studio 2010 的 SSDT** 不再可用，因此请选择较新版本。 新版 SSDT 将通过现有的 Visual Studio 2010 安装并行运行。 SSDT 不必与你计算机上的完整产品版 Visual Studio 匹配。  
  
Visual Studio 2013 客户可以下载预览版本的 SSDT，以试用产品发布版本中尚未包括的新功能。  
  
**SQL BI：Analysis Services、Reporting Services、Integration services**  
  
BI 模板用于创建 SSAS 模型、SSRS 报表和 SSIS 包。 BI Designer 与特定版本的 SQL Server 关联。 若要使用较新的 BI 功能，请安装较新版本的 BI Designer。  
  
**BI Designer**  
  
[下载 SSDT-BI for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)（SQL Server 2014、SQL Server 2012、SQL Server 2008 和 2008 R2）  
  
[下载 SSDT-BI for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)（SQL Server 2014、SQL Server 2012、SQL Server 2008 和 2008 R2）  
  
Business Intelligence Development Studio (BIDS) 通过 SQL Server 安装程序进行安装。 没有 Web 下载。 （SQL Server 2008 和 2008 R2）  
  
对于 SQL Server 2012 或 2014，你可以使用“” **SSDT-BI f或“” Visual Studio 2012** 或“” **SSDT-BI f或“” Visual Studio 2013**。 两者之间唯一的区别在于 Visual Studio 的版本。  
  
## <a name="see-also"></a>另请参阅  
[下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  
[下载 SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[SQL 工具和实用工具](../tools/overview-sql-tools.md)
