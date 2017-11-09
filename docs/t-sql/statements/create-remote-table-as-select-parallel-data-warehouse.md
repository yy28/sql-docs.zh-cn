---
title: "创建远程 TABLE AS SELECT （并行数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a0318d108d6dfaaa374af9a1ab8a148ff960dfcd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>创建远程 TABLE AS SELECT （并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  选择从数据[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]数据库并将该数据复制到的新表中 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]远程服务器上的数据库。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]设备上，使用 MPP 查询处理，若要选择的远程副本的数据的所有好处。 对方案需要使用此[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能。  
  
 若要配置远程服务器，在中看到"远程表复制" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE REMOTE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name     AT ('<connection_string>')  
    [ WITH ( BATCH_SIZE = batch_size ) ]  
    AS <select_statement>  
[;]  
  
<connection_string> ::=   
    Data Source = { IP_address | hostname } [, port ]; User ID = user_name ;Password = password;  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 要创建的远程表中的数据库。 *database_name*是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 默认值是在目标上的用户登录名的默认数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。  
  
 *schema_name*  
 新的表的架构。 默认值是在目标上的用户登录名的默认架构[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。  
  
 *table_name*  
 新的表的名称。 有关详细信息允许表名，请参阅"对象命名规则"中的[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 为堆创建远程表。 它没有 check 约束或触发器。 远程表中各列的排序规则是源表中各列的排序规则相同。 这适用于类型的列**char**， **nchar**， **varchar**，和**nvarchar**。  
  
 *connection_string*  
 指定的字符字符串`Data Source`， `User ID`，和`Password`用于连接到远程服务器和数据库的参数。  
  
 连接字符串是以分号分隔的键和值对的列表。 关键字不区分大小写。 将忽略键和值对之间的空格。 但是，值可能区分大小写，具体取决于数据源。  
  
 *数据源*  
 参数中指定的名称或 IP 地址和 TCP 端口号为远程 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 *主机名*或*IP_address*  
 远程服务器计算机或远程服务器的 IPv4 地址的名称。 不支持 IPv6 地址。 你可以指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]命名格式实例**指定**或**IP_address\Instance_Name**。 服务器必须是远程，并因此不能指定为 （本地）。  
  
 TCP*端口*数  
 连接 TCP 端口号。 你可以指定 TCP 的端口号从 0 到 65535 的未在侦听默认端口 1433年的 SQL Server 实例。 例如： **ServerA，1450年**或**10.192.14.27,1435**  
  
> [!NOTE]  
>  我们建议使用的 IP 地址连接到远程服务器。 根据你的网络配置，通过使用计算机名称连接可能需要其他步骤，使用你的非设备 DNS 服务器的名称解析为正确的服务器。 连接的 IP 地址时，不需要此步骤。 详细信息，请参阅"使用 DNS 转发器来解析非设备 DNS 名称 （分析平台系统）"中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 *user_name*  
 一个有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证登录名。 最大字符数为 128。  
  
 *密码*  
 登录密码。 最大字符数为 128。  
  
 *batch_size*  
 最大每批的行数。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将在批处理中的行发送到目标服务器。 *Batch_size*是一个正整数 > = 0。 默认值为 0。  
  
 与*common_table_expression*  
 指定临时命名的结果集，这些结果集称为公用表表达式 (CTE)。 有关详细信息，请参阅[使用 common_table_expression &#40;Transact SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 选择\<select_criteria > 指定的数据将填充新的远程表的查询谓词。 SELECT 语句的信息，请参阅[选择 &#40;Transact SQL &#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要：  
  
-   SELECT 子句中的每个对象的 SELECT 权限。  
  
-   要求具有 CREATE TABLE 权限目标 SMP 数据库。  
  
-   需要 ALTER、 INSERT 和目标 SMP 架构的 SELECT 权限。  
  
## <a name="error-handling"></a>错误处理  
 如果将数据复制到远程数据库失败，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将中止操作，记录错误，并尝试删除远程表。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]不保证新的表成功清理。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 **远程目标服务器**:  
  
-   TCP 是默认设置，并仅支持协议连接到远程服务器。  
  
-   目标服务器必须是非设备服务器。 CREATE REMOTE TABLE 无法用于将数据复制到另一个设备。  
  
-   CREATE REMOTE TABLE 语句仅创建新表。 因此，新的表不能已存在。 使用远程数据库和架构必须已存在。  
  
-   远程服务器必须具有可用空间来存储的数据传输到设备的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]远程数据库。  
  
 **SELECT 语句**:  
  
-   中的选择条件不支持 ORDER BY 和 TOP 子句。  
  
-   在活动事务内或自动关闭设置为会话处于活动状态时，不能运行 CREATE REMOTE TABLE。  
  
 [设置行计数 &#40;Transact SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)对此语句无效。 若要实现类似的行为，使用[顶部 &#40;Transact SQL &#41;](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="locking-behavior"></a>锁定行为  
 创建远程表后，开始复制之前未锁定目标表。 因此，很可能为另一个进程，则创建它之后，开始复制之前删除远程表。 当发生这种情况时，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将生成错误并复制将失败。  
  
## <a name="metadata"></a>元数据  
 使用[sys.dm_pdw_dms_workers &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)若要查看将所选的数据复制到远程 SMP 服务器的进度。 与类型 PARALLEL_COPY_READER 的行包含此信息。  
  
## <a name="security"></a>安全性  
 CREATE REMOTE TABLE 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证连接到远程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例; 它不使用 Windows 身份验证。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]必须防火墙外部的面向网络发生异常，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]端口、 管理端口和管理端口。  
  
 为了帮助防止意外数据丢失或损坏，用于从设备将复制到目标数据库的用户帐户应具有目标数据库的仅是所需最低的权限。  
  
 连接设置允许你连接到 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例与 SSL 保护用户名称和密码的数据，但未加密以明文形式发送的实际数据。 当发生这种情况时，恶意用户可能会截获 CREATE REMOTE TABLE 语句文本，其中包含[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户名和密码登录到 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 若要避免这种风险，请使用数据加密 SMP 的连接上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。  
  
##  <a name="Examples"></a> 示例  
  
### <a name="a-creating-a-remote-table"></a>A. 创建远程表  
 此示例将创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SMP 远程表调用`MyOrdersTable`数据库上`OrderReporting`和架构`Orders`。 `OrderReporting`数据库位于一个名为服务器`SQLA`侦听默认端口 1433年。 到服务器的连接使用的用户凭据`David`，其密码`e4n8@3`。  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdmpdwdmsworkers-dmv-for-remote-table-copy-status"></a>B. 查询 sys.dm_pdw_dms_workers DMV 的远程表复制状态  
 此查询显示如何查看远程表复制的复制状态。  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. 使用创建远程表的查询联接提示  
 此查询显示使用创建远程表的查询联接提示的基本语法。 查询提交到管理节点中之后, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 计算节点上运行，在生成时，将应用的哈希联接策略[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查询计划。 有关联接提示以及如何使用 OPTION 子句的详细信息，请参阅[OPTION 子句 &#40;Transact SQL &#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  


