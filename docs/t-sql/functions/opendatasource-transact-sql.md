---
title: OPENDATASOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OPENDATASOURCE
- OPENDATASOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENDATASOURCE function
- remote data access [SQL Server], OPENDATASOURCE
- ad hoc distributed queries
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: 5510b846-9cde-4687-8798-be9a273aad31
caps.latest.revision: 41
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b040d7a1ee620702c73c7031b421837073f977b6
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37788038"
---
# <a name="opendatasource-transact-sql"></a>OPENDATASOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  在四部分对象名称中提供连接信息，而不使用链接服务器名称。  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
OPENDATASOURCE ( provider_name, init_string )  
```  
  
## <a name="arguments"></a>参数  
 provider_name  
 注册为用于访问数据源的 OLE DB 访问接口的 PROGID 的名称。 provider_name 的数据类型为 char，并且没有默认值。  
  
 *init_string*  
 连接字符串，该字符串将要传递给目标提供程序的 IDataInitialize 接口。 提供程序字符串语法是以关键字值对为基础的，这些关键字值对由分号隔开，例如：'keyword1=value;keyword2=value'****。  
  
 若要了解提供程序上支持的特定关键字值对，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access SDK。 该文档定义了基本语法。 下表列出了 init_string 参数中最常用的关键字。  
  
|关键字|OLE DB 属性|有效值和说明|  
|-------------|---------------------|----------------------------------|  
|数据源|DBPROP_INIT_DATASOURCE|要连接的数据源的名称。 不同的提供程序用不同的方法对此进行解释。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口，这指示服务器的名称。 对于 Jet OLE DB 访问接口来说，这指示 .mdb 文件或 .xls 文件的完整路径。|  
|位置|DBPROP_INIT_LOCATION|要连接的数据库的位置。|  
|扩展属性|DBPROP_INIT_PROVIDERSTRING|提供程序特定的连接字符串。|  
|连接超时|DBPROP_INIT_TIMEOUT|达到该超时值后，连接尝试将失败。|  
|用户 ID|DBPROP_AUTH_USERID|用于该连接的用户 ID。|  
|Password|DBPROP_AUTH_PASSWORD|用于该连接的密码。|  
|目录|DBPROP_INIT_CATALOG|连接到数据源时的初始或默认的目录名称。|  
|集成安全性|DBPROP_AUTH_INTEGRATED|SSPI，指定 Windows 身份验证|  
  
## <a name="remarks"></a>Remarks  
 仅当 DisallowAdhocAccess 注册表选项针对指定的提供程序显式设置为 0，并且启用 Ad Hoc Distributed Queries 高级配置选项时，OPENDATASOURCE 才可用于访问 OLE DB 数据源中的远程数据。 如果未设置这些选项，则默认行为不允许即席访问。  
  
 OPENDATASOURCE 函数可以在能够使用链接服务器名的相同 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法位置中使用。 因此，可以将 OPENDATASOURCE 用作四部分名称的第一部分，该部分名称引用 SELECT、INSERT、UPDATE 或 DELETE 语句中的表或视图的名称；或者引用 EXECUTE 语句中的远程存储过程。 当执行远程存储过程时，OPENDATASOURCE 应该引用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的另一个实例。 OPENDATASOURCE 不接受参数变量。  
  
 与 OPENROWSET 函数类似，OPENDATASOURCE 应该只引用那些不经常访问的 OLE DB 数据源。 对于访问次数较频繁的任何数据源，请为它们定义链接服务器。 无论 OPENDATASOURCE 还是 OPENROWSET 都不能提供链接服务器定义的全部功能，例如，安全管理以及查询目录信息的功能。 每次调用 OPENDATASOURCE 时，都必须提供所有的连接信息（包括密码）。  
  
> [!IMPORTANT]  
>  Windows 身份验证比 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证要安全得多。 应尽量使用 Windows 身份验证。 OPENDATASOURCE 不应该用于连接字符串中的显式密码。  
  
 每个提供程序的连接要求与创建链接服务器时的参数要求相似。 在 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 主题中列出了很多常见提供程序的详细信息。  
  
 FROM 子句中对 OPENDATASOURCE、OPENQUERY 或 OPENROWSET 的任何调用与对用作更新目标的这些函数的任何调用都是分开独立计算的，即使为两个调用提供的参数相同也是如此。 具体而言，应用到上述任一调用的结果的筛选器或联接条件不会影响其他调用的结果。  
  
## <a name="permissions"></a>权限  
 任何用户都可以执行 OPENDATASOURCE。 用于连接到远程服务器的权限由连接字符串确定。  
  
## <a name="examples"></a>示例  
 以下示例将创建与服务器 `Payroll` 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例 `London` 的即席连接，并查询 `AdventureWorks2012.HumanResources.Employee` 表。 （使用 SQLNCLI 并且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将重定向到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口的最新版本。）  
  
```  
SELECT *  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=London\Payroll;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Employee  
```  
  
 以下示例以 1997 - 2003 格式创建与 Excel 电子表格的即席连接。  
  
```  
SELECT * FROM OPENDATASOURCE('Microsoft.Jet.OLEDB.4.0',  
'Data Source=C:\DataFolder\Documents\TestExcel.xls;Extended Properties=EXCEL 5.0')...[Sheet1$] ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  
