---
title: 备份和还原使用 Always Encrypted 的数据库 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9176052b413293d25acd7696701e4f118adba03f
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595722"
---
# <a name="backup-and-restore-databases-using-always-encrypted"></a>备份和还原使用 Always Encrypted 的数据库 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本文介绍如何备份和还原包含使用 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) 保护的列的数据库。

备份数据库时，生成的备份文件包含加密列以及 Always Encrypted 密钥的所有元数据。

还原数据库时，会还原所有加密数据和 Always Encrypted 密钥的所有元数据。 

如果在不同服务器上或是采用不同名称还原数据库，则不需要执行任何特殊操作，即可使应用程序可以在目标数据库中查询加密数据，因为这两个数据库中的密钥相同。

有关如何备份和还原数据库的详细信息，请参阅：
- [备份概述 (SQL Server)](../../backup-restore/backup-overview-sql-server.md)
- [将数据库还原到托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started-restore)

## <a name="next-steps"></a>Next Steps
- [通过 SQL Server Management Studio 查询使用 Always Encrypted 的列](always-encrypted-query-columns-ssms.md)
- [使用具有安全 enclave 的 Always Encrypted 开发应用程序](always-encrypted-enclaves-client-development.md) 

## <a name="see-also"></a>另请参阅
- [始终加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [导出和导入使用 Always Encrypted 的数据库](always-encrypted-migrate-using-bacpac.md)
- [通过 SQL Server 导入和导出向导在使用 Always Encrypted 的列之间迁移数据](always-encrypted-migrate-using-import-export-wizard.md)
- [使用 Always Encrypted 将加密数据批量加载到列中](migrate-sensitive-data-protected-by-always-encrypted.md)
