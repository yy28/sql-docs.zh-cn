---
title: SQL Server 加密 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], about encryption
- security [SQL Server], encryption
- cryptography [SQL Server], about cryptography
ms.assetid: ead0150e-4943-4ad5-84c8-36f85c7278f4
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: f2aa6c25f8e8741308ff8f8b5df93cb2af67ad91
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957091"
---
# <a name="sql-server-encryption"></a>SQL Server 加密
  加密是指通过使用密钥或密码对数据进行模糊处理的过程。 这会使数据变得毫无用处，除非使用对应的解密密钥或密码。 加密并不解决访问控制问题。 不过，它可以通过限制数据丢失来增强安全性，即使在访问控制失效的情况下。 例如，如果数据库主机配置有误且黑客获取了敏感数据，则如果数据已加密，那么被盗信息可能会毫无用处。  
  
 您可以在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中为连接、数据和存储过程使用加密。 下表包含有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的加密的详细信息。  
  
> [!IMPORTANT]  
>  虽然加密是可帮助确保安全性的有力工具，但它并不适用于所有数据或连接。 在决定是否实现加密时，请考虑用户访问数据的方式。 如果用户通过公共网络访问数据，则可能需要使用数据加密以增强安全性。 但是，如果所有访问都具有某项安全 Intranet 配置，则可能不需要使用加密。 任何时候使用加密时还应包括密码、密钥和证书的维护策略。  
  
## <a name="in-this-section"></a>本节内容  
 [加密层次结构](encryption-hierarchy.md)  
 提供有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的加密层次结构的信息。  
  
 [选择加密算法](choose-an-encryption-algorithm.md)  
 说明如何选择有效的加密算法。  
  
 [透明数据加密 &#40;TDE&#41;](transparent-data-encryption.md)  
 提供有关如何以透明方式来加密数据的一般信息。  
  
 [SQL Server 和数据库加密密钥 &#40;数据库引擎&#41;](sql-server-and-database-encryption-keys-database-engine.md)  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，加密密钥包括一组用来保护敏感数据的公钥、私钥和对称密钥。 该部分介绍如何实现和管理加密密钥。  
  
## <a name="related-content"></a>相关内容  
 [保护 SQL Server](../securing-sql-server.md)  
 简要介绍如何帮助确保 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 平台的安全性以及如何处理用户和安全对象。  
  
 [&#40;Transact-sql 的加密函数&#41;](/sql/t-sql/functions/cryptographic-functions-transact-sql)  
 说明如何实现加密函数。  
  
 [ENCRYPTBYPASSPHRASE &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
 说明如何使用密码来加密数据。  
  
 [ENCRYPTBYKEY &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbykey-transact-sql)  
 说明如何使用对称密钥来加密数据。  
  
 [ENCRYPTBYASYMKEY &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
 说明如何使用非对称密钥来加密数据。  
  
 [ENCRYPTBYCERT &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbycert-transact-sql)  
 说明如何使用证书来加密数据。  
  
## <a name="external-resources"></a>外部资源  
 [SQL Server 2005 安全的10个步骤](https://www.itprotoday.com/sql-server/10-steps-sql-server-2005-security)  
 包含有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全性的最新信息。  
  
## <a name="see-also"></a>另请参阅  
 [sys. key_encryptions &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-key-encryptions-transact-sql)   
 [SQL Server 和数据库加密密钥 &#40;数据库引擎&#41;](sql-server-and-database-encryption-keys-database-engine.md)   
 [备份和还原 Reporting Services 加密密钥](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  
