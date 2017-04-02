---
title: "选择加密算法 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "加密 [SQL Server], 算法"
  - "加密 [SQL Server], 算法"
  - "安全性 [SQL Server], 加密"
  - "算法 [SQL Server 加密]"
ms.assetid: 8227028c-a9c9-489d-bd27-fbf8242634ae
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 选择加密算法
  加密是希望保护 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例安全的管理员可以采用的多种深度防御方法之一。  
  
 加密算法定义了未经授权的用户无法轻易逆转的数据转换。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 允许管理员和开发人员从多种算法中进行选择，其中包括 DES、Triple DES、TRIPLE_DES_3KEY、RC2、RC4、128 位 RC4、DESX、128 位 AES、192 位 AES 和 256 位 AES。  
  
> [!NOTE]  
>  从 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 开始，除 AES_128、AES_192 和 AES_256 以外的所有算法都已过时。 若要使用旧算法（不推荐），必须将数据库设置为兼容级别 120 或更低。  
  
 没有一种算法能够解决所有问题，有关每种算法的优势的说明不属于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 联机丛书的讨论范畴。 但是，下列一般原则适应于：  
  
-   强加密通常会比较弱的加密占用更多的 CPU 资源。  
  
-   长密钥通常会比短密钥生成更强的加密。  
  
-   非对称加密比使用相同密钥长度的对称加密更弱，但速度相对较慢。  
  
-   使用长密钥的块密码比流密码更强。  
  
-   复杂的长密码比短密码更强。  
  
-   如果您正在加密大量数据，应使用对称密钥来加密数据，并使用非对称密钥来加密该对称密钥。  
  
-   不能压缩已加密的数据，但可以加密已压缩的数据。 如果使用压缩，应在加密前压缩数据。  
  
> [!IMPORTANT]  
>  RC4 算法仅用于支持向后兼容性。 仅当数据库兼容级别为 90 或 100 时，才能使用 RC4 或 RC4_128 对新材料进行加密。 （建议不要使用。）而是使用一种较新的算法，如 AES 算法之一。 在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和更高版本中，可以在任何兼容级别对使用 RC4 或 RC4_128 加密的材料进行解密。  
>   
>  对不同数据块重复使用相同的 RC4 或 RC4_128 KEY_GUID 将导致产生相同的 RC4 密钥，因为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不自动提供 salt。 重复使用相同的 RC4 密钥是已知错误，将导致加密非常不可靠。 因此，不推荐使用 RC4 和 RC4_128 关键字。 [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)]  
  
 有关加密算法和加密技术的详细信息，请参阅 MSDN 的 .NET Framework 开发人员指南中的 [重要安全性概念](http://go.microsoft.com/fwlink/?LinkId=62082) 。  
  
 **关于 DES 算法的说明：**  
  
-   DESX 的命名不正确。 使用 ALGORITHM = DESX 创建的对称密钥实际上使用的是具有 192 位密钥的 TRIPLE DES 密码。 不提供 DESX 算法。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   使用 ALGORITHM = TRIPLE_DES_3KEY 创建的对称密钥使用的是具有 192 位密钥的 TRIPLE DES。  
  
-   使用 ALGORITHM = TRIPLE_DES 创建的对称密钥使用的是具有 128 位密钥的 TRIPLE DES。  
  
## 相关任务  
  
|||  
|-|-|  
|使用对称密钥加密。|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|使用非对称密钥加密。|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|使用证书加密。|[CREATE CERTIFICATE (Transact-SQL)](../../../t-sql/statements/create-certificate-transact-sql.md)|  
|使用透明数据加密对数据库文件进行加密。|[透明数据加密 (TDE)](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)|  
|如何加密表中的列。|[加密数据列](../../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
## 另请参阅  
 [SQL Server 加密](../../../relational-databases/security/encryption/sql-server-encryption.md)   
 [加密层次结构](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  