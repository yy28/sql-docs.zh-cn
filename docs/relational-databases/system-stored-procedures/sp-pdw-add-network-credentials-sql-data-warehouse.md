---
title: sp_pdw_add_network_credentials （SQL 数据仓库） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7f2dfe569a163b7a8268f925a5f48849778b3454
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2018
ms.locfileid: "36886983"
---
# <a name="sppdwaddnetworkcredentials-sql-data-warehouse"></a>sp_pdw_add_network_credentials （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  这会存储中的网络凭据[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]并将其与服务器相关联。 例如，使用此存储的过程以便[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]相应的读/写权限来执行数据库备份和还原操作在目标服务器上，或者创建用于 TDE 的证书的备份。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', ꞌpasswordꞌ  
```  
  
## <a name="arguments"></a>参数  
 '*target_server_name*'  
 指定的目标服务器主机名或 IP 地址。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 将使用传递给此存储过程的用户名和密码凭据访问此服务器。  
  
 若要通过 InfiniBand 网络连接，请使用目标服务器的 InfiniBand IP 地址。  
  
 *target_server_name*定义为 nvarchar(337)。  
  
 '*user_name*'  
 指定有权访问目标服务器的用户名。 如果目标服务器的凭据已存在，它们将更新为新的凭据。  
  
 *user_name*定义为 nvarchar (513)。  
  
 '*密码*ꞌ  
 指定的密码*user_name*。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="permissions"></a>权限  
 需要**ALTER SERVER STATE**权限。  
  
## <a name="error-handling"></a>错误处理  
 如果在控制节点和所有计算节点上未成功添加凭据，就会出错。  
  
## <a name="general-remarks"></a>一般备注  
 此存储的过程将网络凭据添加到的 NetworkService 帐户[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 NetworkService 帐户运行每个实例 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]控制节点和计算节点上。 例如，备份操作运行时，控制节点和每个计算节点将使用 NetworkService 帐户凭据来获取读取并写入到目标服务器的权限。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>A. 添加用于执行数据库备份的凭据  
 下面的示例将域用户 seattle\david 用户名和密码凭据与具有 10.172.63.255 的 IP 地址的目标服务器相关联。 用户 seattle\david 具有读/写到目标服务器的权限。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 将存储这些凭据，并使用它们来读取和写入到和从目标服务器，根据需要为备份和还原操作。  
  
```  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 备份命令需要一个 IP 地址，输入服务器名称。  
  
> [!NOTE]  
>  若要通过 InfiniBand 执行数据库备份，请务必使用备份服务器的 InfiniBand IP 地址。  
  
## <a name="see-also"></a>请参阅  
 [sp_pdw_remove_network_credentials &#40;SQL 数据仓库&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

