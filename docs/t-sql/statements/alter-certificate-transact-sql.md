---
title: ALTER CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/18/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_CERTIFICATE_TSQL
- ALTER CERTIFICATE
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- encryption [SQL Server], certificates
- modifying certificates
- private keys [SQL Server]
- ALTER CERTIFICATE statement
- certificates [SQL Server], modifying
ms.assetid: da4dc25e-72e0-4036-87ce-22de83160836
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1e83bc2c83f654ae82ed5a84c33f5801c5a06549
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781335"
---
# <a name="alter-certificate-transact-sql"></a>ALTER CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  更改用于加密证书的私钥，如果不存在则添加私钥。 更改证书对于 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的可用性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER CERTIFICATE certificate_name   
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY ( <private_key_spec> [ ,... ] )  
    | WITH ACTIVE FOR BEGIN_DIALOG = [ ON | OFF ]  
  
<private_key_spec> ::=   
      FILE = 'path_to_private_key'   
    | DECRYPTION BY PASSWORD = 'key_password'   
    | ENCRYPTION BY PASSWORD = 'password'   
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER CERTIFICATE certificate_name   
{  
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY (   
        FILE = '<path_to_private_key>',  
        DECRYPTION BY PASSWORD = '<key password>' )
}  
```  
  
## <a name="arguments"></a>参数  
 certificate_name  
 在数据库中标识证书的唯一名称。  
  
 FILE **='**_path\_to\_private\_key_**'**  
 指定私钥的完整路径（包括文件名）。 此参数可以是本地路径或网络位置的 UNC 路径。 将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户的安全上下文中访问此文件。 使用此选项时，必须确保服务帐户有权访问指定的文件。  
  
 DECRYPTION BY PASSWORD **='**_key\_password_**'**  
 指定解密私钥所需的密码。  
  
 ENCRYPTION BY PASSWORD ='password'  
 指定用于对数据库中的证书私钥进行加密的密码。 password 必须符合运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机的 Windows 密码策略要求。 有关详细信息，请参阅 [Password Policy](../../relational-databases/security/password-policy.md)。  
  
 REMOVE PRIVATE KEY   
 指定私钥不应再保留在数据库内。  
  
 ACTIVE FOR BEGIN_DIALOG = { ON | OFF }  
 使证书可用于 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 对话会话的发起方。  
  
## <a name="remarks"></a>Remarks  
 私钥必须与 certificate_name 指定的公钥相对应。  
  
 如果文件中的密码受空密码保护，则可省略 DECRYPTION BY PASSWORD 子句。  
  
 在从文件中导入数据库已存在的证书私钥时，该私钥将自动受到数据库主密钥的保护。 若要使用密码保护私钥，请使用 ENCRYPTION BY PASSWORD 短语。  
  
 REMOVE PRIVATE KEY 选项将从数据库中删除证书的私钥。 当使用证书来验证签名或在不需要私钥的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 方案中时，可以删除私钥。 请勿删除保护对称密钥的证书的私钥。  
  
 如果使用数据库主密钥加密私钥，则不必指定解密密码。  
  
> [!IMPORTANT]  
>  从数据库删除私钥前，始终对其建立存档副本。 有关详细信息，请参阅 [BACKUP CERTIFICATE (Transact-SQL)](../../t-sql/statements/backup-certificate-transact-sql.md)。  
  
 WITH PRIVATE KEY 选项在包含的数据库中不可用。  
  
## <a name="permissions"></a>Permissions  
 需要对证书具有 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-password-of-a-certificate"></a>A. 更改证书的密码  
  
```  
ALTER CERTIFICATE Shipping04   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = 'pGF$5DGvbd2439587y',  
    ENCRYPTION BY PASSWORD = '4-329578thlkajdshglXCSgf');  
GO  
```  
  
### <a name="b-changing-the-password-that-is-used-to-encrypt-the-private-key"></a>B. 更改用于加密私钥的密码  
  
```  
ALTER CERTIFICATE Shipping11   
    WITH PRIVATE KEY (ENCRYPTION BY PASSWORD = '34958tosdgfkh##38',  
    DECRYPTION BY PASSWORD = '95hkjdskghFDGGG4%');  
GO  
```  
  
### <a name="c-importing-a-private-key-for-a-certificate-that-is-already-present-in-the-database"></a>C. 为数据库中已存在的证书导入私钥  
  
```  
ALTER CERTIFICATE Shipping13   
    WITH PRIVATE KEY (FILE = 'c:\\importedkeys\Shipping13',  
    DECRYPTION BY PASSWORD = 'GDFLKl8^^GGG4000%');  
GO  
```  
  
### <a name="d-changing-the-protection-of-the-private-key-from-a-password-to-the-database-master-key"></a>D. 将私钥保护从密码更改为数据库主密钥  
  
```  
ALTER CERTIFICATE Shipping15   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hk000eEnvjkjy#F%');  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)   
 [DROP CERTIFICATE (Transact-SQL)](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE (Transact-SQL)](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

