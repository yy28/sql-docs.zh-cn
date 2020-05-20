---
title: sys. sp_rda_reauthorize_db （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 68267f07c125e05f235c1a0bcb4c7f855274bc86
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814701"
---
# <a name="syssp_rda_reauthorize_db-transact-sql"></a>sys.sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  还原已启用延伸的本地数据库与远程数据库之间经过身份验证的连接。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>参数  
 @credential= * \@ 凭据*  
 与启用 Stretch 的本地数据库关联的数据库范围凭据。  
  
 @with_copy= * \@ with_copy*  
 指定是否创建远程数据的副本并连接到副本（推荐）。 * \@ with_copy*为 bit。  
  
 @azure_servername= * \@ azure_servername*  
 指定包含远程数据的 Azure 服务器的名称。 * \@ azure_servername* sysname。  
  
 @azure_databasename= * \@ azure_databasename*  
 指定包含远程数据的 Azure 数据库的名称。 * \@ azure_databasename* sysname。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0 （失败）  
  
## <a name="permissions"></a>权限  
 需要 db_owner 权限。  
  
## <a name="remarks"></a>备注  
 当你运行[sp_rda_reauthorize_db （transact-sql）](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)以重新连接到远程 Azure 数据库时，此操作会自动将查询模式重置为 LOCAL_AND_REMOTE，这是 Stretch Database 的默认行为。 也就是说，查询从本地和远程数据返回结果。  
  
## <a name="example"></a>示例  
 下面的示例将还原为 Stretch 启用的本地数据库和远程数据库之间经过身份验证的连接。 它创建远程数据的副本（推荐），并连接到新副本。  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys. sp_rda_deauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
