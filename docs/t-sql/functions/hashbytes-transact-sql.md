---
title: HASHBYTES (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HASHBYTES_TSQL
- HASHBYTES
dev_langs:
- TSQL
helpviewer_keywords:
- hash input
- HASHBYTES
ms.assetid: 0ea6a4d1-313e-4f70-b939-dd2cd570f6d6
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 60586f787d405b18b7a0ba66e666204fca51050c
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39456151"
---
# <a name="hashbytes-transact-sql"></a>HASHBYTES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回其在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的输入的 MD2、MD4、MD5、SHA、SHA1 或 SHA2 哈希值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
HASHBYTES ( '<algorithm>', { @input | 'input' } )  
  
<algorithm>::= MD2 | MD4 | MD5 | SHA | SHA1 | SHA2_256 | SHA2_512   
```  
  
## <a name="arguments"></a>参数  
 **'**\<algorithm>**'**  
 标识用于对输入执行哈希操作的哈希算法。 这是必选参数，无默认值。 需要使用单引号。 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 开始，除 SHA2_256 和 SHA2_512 以外的所有算法都已过时。 较旧算法（不推荐）将继续工作，但它们将引发弃用事件。  
  
 **@input**  
 指定包含要对其执行哈希操作的数据的变量。 @input 为 varchar、nvarchar 或 varbinary。  
  
 **'** input **'**  
 指定一个表达式，其计算结果为要对其执行哈希操作的字符或二进制字符串。  
  
 输出符合算法标准：MD2、MD4 和 MD5 为 128 位（即 16 个字节）；SHA 和 SHA1 为 160 位（即 20 个字节）；SHA2_256 为 256 位（即 32 个字节），SHA2_512 为 512 位（即 64 个字节）。  
  
适用范围：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 对于 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和更早版本，允许的输入值限制为 8000 个字节。  
  
## <a name="return-value"></a>返回值  
 varbinary（最大 8000 个字节）  
  
## <a name="examples"></a>示例  
  
### <a name="a-return-the-hash-of-a-variable"></a>A：返回变量的哈希  
 以下示例返回变量 `@HashThis` 中存储的 nvarchar 数据的 `SHA1` 哈希值。  
  
```  
DECLARE @HashThis nvarchar(4000);  
SET @HashThis = CONVERT(nvarchar(4000),'dslfdkjLK85kldhnv$n000#knf');  
SELECT HASHBYTES('SHA1', @HashThis);  
  
```  
  
### <a name="b-return-the-hash-of-a-table-column"></a>B：返回表列的哈希  
 下面的示例返回 `c1` 表 `Test1` 列中值的 SHA1 哈希。  
  
```  
CREATE TABLE dbo.Test1 (c1 nvarchar(50));  
INSERT dbo.Test1 VALUES ('This is a test.');  
INSERT dbo.Test1 VALUES ('This is test 2.');  
SELECT HASHBYTES('SHA1', c1) FROM dbo.Test1;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
-------------------------------------------  
0x0E7AAB0B4FF0FD2DFB4F0233E2EE7A26CD08F173  
0xF643A82F948DEFB922B12E50B950CEE130A934D6  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [选择加密算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
