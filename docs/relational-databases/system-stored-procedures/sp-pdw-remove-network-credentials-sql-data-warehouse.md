---
title: "sp_pdw_remove_network_credentials （SQL 数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a82cc5004304310c7c2bc3392ada6bad0acb617f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sppdwremovenetworkcredentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  这将删除存储在中的网络凭据[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]访问的网络文件共享。 例如，使用此存储的过程来删除权限[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]执行备份和还原位于您自己的网络内的服务器上的操作。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```  
  
## <a name="arguments"></a>参数  
 '*target_server_name*'  
 指定的目标服务器主机名或 IP 地址。 凭据来访问此服务器将不再从[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 这不会更改或删除由你自己的团队管理的实际目标服务器上的任何权限。  
  
 *target_server_name*定义为 nvarchar(337)。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="permissions"></a>权限  
 需要**更改服务器状态**权限。  
  
## <a name="error-handling"></a>错误处理  
 如果删除凭据将不会成功在管理节点和所有计算节点上，则会发生错误。  
  
## <a name="general-remarks"></a>一般备注  
 此存储的过程从的 NetworkService 帐户中删除网络凭据[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 NetworkService 帐户运行每个实例的 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]控制节点和计算节点上。 例如，备份操作运行时，管理节点和每个计算节点将使用 NetworkService 帐户凭据来访问目标服务器。  
  
## <a name="metadata"></a>元数据  
 若要列出所有凭据并验证是否已删除的凭据，请使用[sys.dm_pdw_network_credentials &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
 若要添加凭据，使用[sp_pdw_add_network_credentials &#40;SQL 数据仓库 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. 删除用于执行数据库备份的凭据  
 下面的示例删除用于访问目标服务器，它具有 10.192.147.63 的 IP 地址的用户名和密码凭据。  
  
```  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

