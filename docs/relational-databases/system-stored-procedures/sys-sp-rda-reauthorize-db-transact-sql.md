---
title: sys.sp_rda_reauthorize_db (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9991ad7e43ffa367387392b40a22a1bea9aed37c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407506"
---
# <a name="syssprdareauthorizedb-transact-sql"></a>sys.sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  还原启用了 Stretch 和远程数据库的本地数据库之间的经过身份验证的连接。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>参数  
 @credential = *@credential*  
 是与本地的已启用延伸的数据库相关联的数据库范围凭据。  
  
 @with_copy = *@with_copy*  
 指定是否要进行远程数据的副本并连接到副本 （推荐）。 *@with_copy* 类型为 bit。  
  
 @azure_servername = *@azure_servername*  
 指定包含远程数据的 Azure 服务器的名称。 *@azure_servername* 数据类型为 sysname。  
  
 @azure_databasename = *@azure_databasename*  
 指定包含远程数据的 Azure 数据库的名称。 *@azure_databasename* 数据类型为 sysname。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0（失败）  
  
## <a name="permissions"></a>权限  
 需要 db_owner 权限。  
  
## <a name="remarks"></a>Remarks  
 在运行时[sys.sp_rda_reauthorize_db (Transact SQL)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新连接到远程 Azure 数据库，此操作会自动重置查询模式 LOCAL_AND_REMOTE，到这是 Stretch Database 的默认行为。 也就是说，查询返回结果从本地和远程数据。  
  
## <a name="example"></a>示例  
 下面的示例还原启用了 Stretch 和远程数据库的本地数据库之间的经过身份验证的连接。 它生成 （建议） 的远程数据的副本并连接到新的副本。  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>请参阅  
 [sys.sp_rda_deauthorize_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
