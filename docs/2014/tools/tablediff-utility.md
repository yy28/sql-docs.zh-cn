---
title: tablediff 实用工具 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- comparing data
- tablediff utility
- tables [SQL Server replication]
- table comparisons [SQL Server]
- command prompt utilities [SQL Server], tablediff
- troubleshooting [SQL Server replication], non-convergence
- non-convergence [SQL Server]
ms.assetid: 3c3cb865-7a4d-4d66-98f2-5935e28929fc
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a6d073e95d896429e1827009c249b940ade2e7b9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180964"
---
# <a name="tablediff-utility"></a>tablediff 实用工具
  **tablediff** 实用工具用于比较两个非收敛表中的数据，它对于排除复制拓扑中的非收敛故障非常有用。 可以从命令提示符或在批处理文件中使用该实用工具执行以下任务：  
  
-   在充当复制发布服务器的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例中的源表与充当复制订阅服务器的一个或多个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例中的目标表之间进行逐行比较。  
  
-   通过只比较行数和架构可以执行快速比较。  
  
-   执行列级比较。  
  
-   生成 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本，用以修复目标服务器中的差异，以使源表和目标表实现收敛。  
  
-   将结果记录到输出文件或目标数据库的表中。  
  
## <a name="syntax"></a>语法  
  
```  
  
      tablediff   
[ -? ] |   
{  
        -sourceserversource_server_name[\instance_name]  
        -sourcedatabasesource_database-sourcetablesource_table_name   
    [ -sourceschemasource_schema_name ]  
    [ -sourcepasswordsource_password ]  
    [ -sourceusersource_login ]  
    [ -sourcelocked ]  
        -destinationserverdestination_server_name[\instance_name]  
        -destinationdatabasesubscription_database-destinationtabledestination_table   
    [ -destinationschemadestination_schema_name ]  
    [ -destinationpassworddestination_password ]  
    [ -destinationuserdestination_login ]  
    [ -destinationlocked ]  
    [ -blarge_object_bytes ]   
    [ -bfnumber_of_statements ]   
    [ -c ]   
    [ -dt ]   
    [ -ettable_name ]   
    [ -f [ file_name ] ]   
    [ -ooutput_file_name ]   
    [ -q ]   
    [ -rcnumber_of_retries ]   
    [ -riretry_interval ]   
    [ -strict ]  
    [ -tconnection_timeouts ]   
}  
```  
  
## <a name="arguments"></a>参数  
 [ **-?** ]  
 返回支持参数的列表。  
  
 **-sourceserver** *source_server_name*[**\\***instance_name*]  
 源服务器的名称。 指定 *默认实例的* source_server_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 命名实例的 source_server_name\\instance_name**。  
  
 **-sourcedatabase** *source_database*  
 源数据库的名称。  
  
 **-sourcetable** *source_table_name*  
 正在检查的源表的名称。  
  
 **-sourceschema** *source_schema_name*  
 源表的架构所有者。 默认情况下，表所有者假定为 dbo。  
  
 **-sourcepassword** *source_password*  
 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证连接到源服务器时所使用的登录帐户的密码。  
  
> [!IMPORTANT]  
>  可能的话，请在运行时提供安全凭据。 如果必须在脚本文件中存储凭据，则应保护文件以防止未经授权的访问。  
  
 **-sourceuser** *source_login*  
 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证连接到源服务器时所使用的登录帐户。 如果未提供 *source_login* ，则连接到源服务器时使用 Windows 身份验证。 [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-sourcelocked**  
 在使用 TABLOCK 和 HOLDLOCK 表提示的比较过程中锁定源表。  
  
 **-destinationserver** *destination_server_name*[**\\***instance_name*]  
 目标服务器的名称。 指定 *destination_server_name* source_server_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 命名实例的 destination_server_name\\instance_name**。  
  
 **-destinationdatabase** *subscription_database*  
 目标数据库的名称。  
  
 **-destinationtable** *destination_table*  
 目标表的名称。  
  
 **-destinationschema** *destination_schema_name*  
 目标表的架构所有者。 默认情况下，表所有者假定为 dbo。  
  
 **-destinationpassword** *destination_password*  
 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证连接到目标服务器时所使用的登录帐户的密码。  
  
> [!IMPORTANT]  
>  可能的话，请在运行时提供安全凭据。 如果必须在脚本文件中存储凭据，则应保护文件以防止未经授权的访问。  
  
 **-destinationuser** *destination_login*  
 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证连接到目标服务器时所使用的登录帐户。 如果未提供 *destination_login* ，则连接到该服务器时使用 Windows 身份验证。 [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-destinationlocked**  
 在使用 TABLOCK 和 HOLDLOCK 表提示的比较过程中锁定目标表。  
  
 **-b** *large_object_bytes*  
 是字节数进行比较的大型对象数据类型列，其中包括： `text`， `ntext`， `image`， `varchar(max)`，`nvarchar(max)`和`varbinary(max)`。 *large_object_bytes* 默认为列的大小。 任何大于 *large_object_bytes* 的数据不会进行比较。  
  
 **-bf**  *number_of_statements*  
 使用 [!INCLUDE[tsql](../includes/tsql-md.md)] -f [!INCLUDE[tsql](../includes/tsql-md.md)] 选项时要写入到当前 **脚本文件中的** 语句数。 当 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句数超过 *number_of_statements*时，将创建一个新的 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本文件。  
  
 **-c**  
 比较列级差异。  
  
 **-dt**  
 删除 *table_name*指定的结果表（如果该表已经存在）。  
  
 **-et** *table_name*  
 指定要创建的结果表的名称。 如果该表已经存在，则必须使用 **-DT** ，否则操作将失败。  
  
 **-f** [ *file_name* ]  
 生成 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本，以使目标服务器中的表与源服务器中的表实现收敛。 （可选）可以指定生成的 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本文件的名称和路径。 如果未指定 *file_name* ，则会在运行实用工具的目录中生成 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本文件。  
  
 **-o** *output_file_name*  
 输出文件的完整名称和路径。  
  
 **-q**  
 通过只比较行数和架构可以执行快速比较。  
  
 **-rc** *number_of_retries*  
 实用工具重试失败操作的次数。  
  
 **-ri**  *retry_interval*  
 两次重试之间的等待间隔（秒）。  
  
 **-strict**  
 对源架构和目标架构进行严格比较。  
  
 **-t** *connection_timeouts*  
 设置与源服务器和目标服务器连接时的连接超时时间（秒）。  
  
## <a name="return-value"></a>返回值  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|成功|  
|**1**|严重错误|  
|**2**|存在表差异|  
  
## <a name="remarks"></a>Remarks  
 **tablediff** 实用工具不能用于非[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务器。  
  
 使用表`sql_variant`不支持数据类型列。  
  
 默认情况下， **tablediff** 实用工具支持源列和目标列之间的以下数据类型映射。  
  
|源数据类型|目标数据类型|  
|----------------------|---------------------------|  
|`tinyint`|`smallint`、`int` 或 `bigint`|  
|`smallint`|`int` 或 `bigint`|  
|`int`|`bigint`|  
|`timestamp`|`varbinary`|  
|`varchar(max)`|`text`|  
|`nvarchar(max)`|`ntext`|  
|`varbinary(max)`|`image`|  
|`text`|`varchar(max)`|  
|`ntext`|`nvarchar(max)`|  
|`image`|`varbinary(max)`|  
  
 使用 **-strict** 选项可禁止这些映射，并执行严格验证。  
  
 进行比较的源表必须至少包含一个主键、标识或 ROWGUID 列。 使用 **-strict** 选项时，目标表也必须具有一个主键、标识或 ROWGUID 列。  
  
 所生成的使目标表实现收敛的 [!INCLUDE[tsql](../includes/tsql-md.md)] 脚本不包括下列数据类型：  
  
-   `varchar(max)`  
  
-   `nvarchar(max)`  
  
-   `varbinary(max)`  
  
-   `timestamp`  
  
-   **xml**  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
## <a name="permissions"></a>权限  
 若要比较表，您必须有要比较的表对象的 SELECT ALL 权限。  
  
 若要使用 **-et** 选项，必须是 db_owner 固定数据库角色的成员，或者在订阅数据库中至少拥有 CREATE TABLE 权限，并且对目标服务器中的目标所有者架构拥有 ALTER 权限。  
  
 若要使用 **-dt** 选项，必须是 db_owner 固定数据库角色的成员，或者至少对目标服务器中的目标所有者架构拥有 ALTER 权限。  
  
 若要使用 **-o** 或 **-f** 选项，必须对指定的文件目录位置拥有写入权限。  
  
## <a name="see-also"></a>请参阅  
 [比较所复制表的差异（复制编程）](../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)  
  
  
