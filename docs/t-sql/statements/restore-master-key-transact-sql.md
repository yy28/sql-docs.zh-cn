---
title: "还原 MASTER KEY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE_MASTER_KEY_TSQL
- RESTORE MASTER KEY
- LOAD_MASTER_KEY_TSQL
- LOAD MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- database master key [SQL Server], importing
- encryption [SQL Server], Database Master Key
- copying Database Master Keys
- importing Database Master Keys
- cryptography [SQL Server], Database Master Key
- transferring Database Master Keys
- RESTORE MASTER KEY statement
ms.assetid: 70ceb951-31a2-4fc4-a0c1-e6c18eeb3ae7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 63c0d492da379f3cb0d982e5f35a2a110a3a6dda
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="restore-master-key-transact-sql"></a>RESTORE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从备份文件中导入数据库主密钥。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
RESTORE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password'  
    ENCRYPTION BY PASSWORD = 'password'  
    [ FORCE ]  
```  
  
## <a name="arguments"></a>参数  
 文件 =*path_to_file*  
 指定存储数据库主密钥的完整路径（包括文件名）。 *path_to_file*可以是本地路径或网络位置的 UNC 路径。  
  
 DECRYPTION BY PASSWORD =*密码*  
 指定对从文件中导入的数据库主密钥进行解密时所需的密码。  
  
 ENCRYPTION BY PASSWORD =*密码*  
 指定用于在将数据库主密钥加载到数据库之后对该密钥进行加密的密码。  
  
 FORCE  
 指定即使当前数据库主密钥未打开，或者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法对使用该主密钥加密的某些私钥进行解密，RESTORE 过程也应继续执行。  
  
## <a name="remarks"></a>注释  
 还原主密钥之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会对使用当前活动的主密钥加密的所有密钥进行解密，然后使用还原后的主密钥对这些密钥进行加密。 这种大量消耗资源的操作应当安排在资源需求较低的时段执行。 如果当前的数据库主密钥未打开或无法打开，或者无法对任何使用该主密钥加密的密钥进行解密，则还原操作将失败。  
  
 请仅在主密钥无法恢复或解密失败时，才使用 FORCE 选项。 仅由不可恢复密钥加密的信息将会丢失。  
  
 如果主密钥通过服务主密钥进行加密，则还原后的主密钥也通过该服务主密钥进行加密。  
  
 如果当前数据库中没有主密钥，则 RESTORE MASTER KEY 将创建一个主密钥。 新的主密钥不会自动使用服务主密钥进行加密。  
  
## <a name="permissions"></a>Permissions  
 要求对数据库具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 以下示例还原 `AdventureWorks2012` 数据库的数据库主密钥。  
  
```  
USE AdventureWorks2012;  
RESTORE MASTER KEY   
    FROM FILE = 'c:\backups\keys\AdventureWorks2012_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
    ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
