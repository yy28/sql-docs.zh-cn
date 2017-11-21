---
title: "CREATE MASTER KEY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_MASTER_KEY_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- CREATE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], Database Master Key
- database master key [SQL Server]
- CREATE MASTER KEY statement
- cryptography [SQL Server], Database Master Key
- database master key [SQL Server], creating
ms.assetid: 1710a305-1a4f-48ec-836c-11ffd0356d76
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e051e59ebae464942068521a95a1d5b06389304e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-master-key-transact-sql"></a>CREATE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  创建数据库主密钥。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Parallel Data Warehouse  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password'  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE MASTER KEY [ ENCRYPTION BY PASSWORD ='password' ]
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 密码 =*密码*  
 用于加密数据库主密钥的密码。 *密码*必须符合 Windows 密码策略要求的计算机的运行的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 *密码*中是可选[!INCLUDE[ssSDS](../../includes/sssds-md.md)]和[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。  
  
## <a name="remarks"></a>注释  
 数据库主密钥是指用于保护证书私钥的对称密钥以及数据库中存在的非对称密钥。 当创建主密钥时，会使用 AES_256 算法以及用户提供的密码对其进行加密。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 中，不使用 Triple DES 算法。 若要启用主密钥的自动解密功能，请使用服务主密钥对该主密钥的副本进行加密，并将副本存储在数据库和 master 中。 通常，每当主密钥更改时，便会在不进行提示的情况下更新存储在 master 中的副本。 可以使用 DROP ENCRYPTION BY SERVICE MASTER KEY 选项更改此默认设置[ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md)。 必须使用打开服务主密钥未进行加密的主密钥[OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md)语句和密码。  
  
 master 中 sys.databases 目录视图的 is_master_key_encrypted_by_server 列指示是否使用服务主密钥对数据库主密钥进行加密。  
  
 可以在 sys.symmetric_keys 目录视图中查看有关数据库主密钥的信息。  

对于 SQL Server 并行数据仓库，主密钥通常受服务主密钥和至少一个密码。 如果以物理方式移动到另一个服务器 （日志传送，还原备份，等等） 的数据库，数据库将包含一份 （除非显式使用删除此加密由原始服务器服务主密钥加密的主密钥ALTER 主密钥 DDL)，以及它用在 CREATE MASTER KEY 或后续 ALTER MASTER KEY DDL 操作过程中指定每个密码加密的副本。 若要恢复主要密钥和加密的密钥层次结构的根节点作为使用主密钥之后移动该数据库, 的所有数据，用户必须使用 OPEN MASTER KEY 语句使用用于保护的主密钥的密码之一还原的主密钥，备份或还原备份的原始服务主密钥新服务器上。 

有关[!INCLUDE[ssSDS](../../includes/sssds-md.md)]和[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]，密码保护不被视为是一种安全机制以防止在情况下，数据库可能从一台服务器之间移动，出现数据丢失现象，因为服务主密钥保护主密钥处于由 Microsoft Azure 平台管理。 因此，微波激射器密钥密码中是可选[!INCLUDE[ssSDS](../../includes/sssds-md.md)]和[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。
  
> [!IMPORTANT]  
>  应通过使用来备份主密钥[备份主密钥](../../t-sql/statements/backup-master-key-transact-sql.md)并将备份存储在一个安全的场外位置。  
  
 服务主密钥和数据库主密钥是通过使用 AES-256 算法进行保护的。  
  
## <a name="permissions"></a>Permissions  
 要求对数据库具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 下面的示例创建数据库主密钥当前数据库。 该密钥使用密码 `23987hxJ#KL95234nl0zBe` 进行加密。  
  
```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
GO  
```  

  
## <a name="see-also"></a>另请参阅  
 [sys.symmetric_keys &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [打开主密钥 &#40;Transact SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [删除 MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [关闭 MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  



