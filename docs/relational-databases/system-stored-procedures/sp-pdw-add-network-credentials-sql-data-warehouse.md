---
title: "sp_pdw_add_network_credentials （SQL 数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b1a964e2d026f93ec26a34b2cb7ba5e114886ec
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sppdwaddnetworkcredentials-sql-data-warehouse"></a>sp_pdw_add_network_credentials （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  这将存储中的网络凭据[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]并将它们与服务器相关联。 例如，使用此存储的过程以便[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]相应的读/写权限执行数据库备份和还原操作在目标服务器上，或创建用于 TDE 证书的备份。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', ꞌpasswordꞌ  
```  
  
## <a name="arguments"></a>参数  
 *target_server_name*  
 指定的目标服务器主机名或 IP 地址。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]将通过使用传递到此存储过程的用户名和密码凭据访问此服务器。  
  
 若要通过 InfiniBand 网络连接，请使用目标服务器的 InfiniBand IP 地址。  
  
 *target_server_name*定义为 nvarchar(337)。  
  
 *user_name*  
 指定有权访问目标服务器的用户名。 如果目标服务器的凭据已存在，则它们将更新到新的凭据。  
  
 *user_name*定义为 nvarchar (513)。  
  
 *密码*ꞌ  
 指定的密码*user_name*。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="permissions"></a>Permissions  
 需要**更改服务器状态**权限。  
  
## <a name="error-handling"></a>错误处理  
 如果添加凭据将不会成功在管理节点和所有计算节点上，则会发生错误。  
  
## <a name="general-remarks"></a>一般备注  
 此存储的过程将网络凭据添加到的 NetworkService 帐户[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 NetworkService 帐户运行每个实例的 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]控制节点和计算节点上。 例如，备份操作运行时，管理节点和每个计算节点将使用 NetworkService 帐户凭据获取读取和写入到目标服务器的权限。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>A. 添加执行数据库备份的凭据  
 下面的示例将域用户 seattle\david 用户名和密码凭据与具有 10.172.63.255 的 IP 地址的目标服务器相关联。 用户 seattle\david 具有到目标服务器的读/写权限。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]将存储这些凭据，并使用它们来读取和写入到和从目标服务器，根据需要进行备份和还原操作。  
  
```  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 备份命令需要一个 IP 地址，输入服务器名称。  
  
> [!NOTE]  
>  要在 InfiniBand 执行数据库备份，请务必使用备份的服务器的 InfiniBand IP 地址。  
  
## <a name="see-also"></a>另请参阅  
 [sp_pdw_remove_network_credentials &#40;SQL 数据仓库 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

