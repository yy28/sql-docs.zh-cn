---
title: 设置加密的镜像数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- cryptography [SQL Server], database mirroring
- encryption [SQL Server], database mirroring
- database master key [SQL Server], database mirroring
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 7329a575-be29-46e0-abc6-1344db37920c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2a74adba783f1a52bdd404e11f0f747234c47f4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62754381"
---
# <a name="set-up-an-encrypted-mirror-database"></a>设置加密的镜像数据库

若要对镜像数据库的数据库主密钥启用自动解密，必须提供用于加密该镜像服务器实例的主密钥的口令。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本包括传输密码的机制。 在开始数据库镜像之前，请使用 **sp_control_dbmasterkey_password** 为数据库主密钥创建一个凭据。 必须为要镜像的每个数据库重复此过程。 有关详细信息，请参阅 [sp_control_dbmasterkey_password (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql)。
  
> [!CAUTION]  
>  对于 **sa** 和其他特权级别高的服务器主体无法访问的数据库，不要启用其故障转移解密功能。 可以对数据库进行配置，以便服务主密钥无法对其密钥层次结构进行解密。 对于包含 **sa** 或其他高特权服务器主体不应访问的信息的数据库来说，此选项是一项深层防御措施。 为此类数据库启用故障转移解密将解除此深层防御措施，使 **sa** 和其他高特权服务器主体能够解密该数据库。  


<!-- Note: We cannot append '?view=sql-server-2016' to these, even tho in theory we might want to. -->

## <a name="see-also"></a>请参阅

[sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql)

[CREATE MASTER KEY (Transact-SQL)](/sql/t-sql/statements/create-master-key-transact-sql)

[ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql)

[加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)

[设置数据库镜像 (SQL Server)](database-mirroring-sql-server.md)

