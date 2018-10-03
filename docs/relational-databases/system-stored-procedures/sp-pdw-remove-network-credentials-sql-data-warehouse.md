---
title: sp_pdw_remove_network_credentials （SQL 数据仓库） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 27c91a2e67f8bd9c71ee0dc5ce088ee596c7c765
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746525"
---
# <a name="sppdwremovenetworkcredentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  这会删除存储中的网络凭据[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]访问网络文件共享。 例如，使用此存储的过程来删除权限[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]执行备份和还原操作，驻留在您自己的网络内的服务器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
## <a name="permissions"></a>Permissions  
 需要**ALTER SERVER STATE**权限。  
  
## <a name="error-handling"></a>错误处理  
 如果在控制节点和所有计算节点上未成功删除凭据，就会出错。  
  
## <a name="general-remarks"></a>一般备注  
 此存储的过程删除网络凭据从的 NetworkService 帐户[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 NetworkService 帐户运行每个实例 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]控制节点和计算节点上。 例如，备份操作运行时，控制节点和每个计算节点将使用 NetworkService 帐户凭据来访问目标服务器。  
  
## <a name="metadata"></a>元数据  
 若要列出所有凭据并验证是否已删除凭据，请使用[sys.dm_pdw_network_credentials &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)。  
  
 若要添加凭据，请使用[sp_pdw_add_network_credentials &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. 删除执行数据库备份的凭据  
 以下示例删除用于访问目标服务器的 IP 地址为 10.192.147.63 的用户名和密码凭据。  
  
```  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

