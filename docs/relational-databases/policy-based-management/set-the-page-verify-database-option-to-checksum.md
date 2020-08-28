---
title: 将 PAGE_VERIFY 数据库选项设置为 CHECKSUM | Microsoft Docs
description: 检查 PAGE_VERIFY 选项是否为 CHECKSUM，该选项控制 SQL Server 数据库引擎是否计算校验和以帮助提供数据文件完整性。
ms.custom: ''
ms.date: 08/19/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4dda2b9138882490b1556b9dbb39f71e35767f5f
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646507"
---
# <a name="set-the-page_verify-database-option-to-checksum"></a>将 PAGE_VERIFY 数据库选项设置为 CHECKSUM
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此规则检查 PAGE_VERIFY 数据库选项是否已设置为 CHECKSUM。 为 PAGE_VERIFY 数据库选项启用 CHECKSUM 后， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 会在向磁盘中写入页面时计算整个页面内容的校验并将该值存储在页头中。 从磁盘中读取页时，将重新计算校验和，并与存储在页头中的校验和值进行比较。 这有助于提供高级别的数据文件完整性。  如果对数据库使用 PAGE VERIFY CHECKSUM 选项，当 SQL Server 检测到页面写入磁盘后发生更改时，SQL Server 会在从磁盘读取回该页面后报告[消息 824](../errors-events/mssqlserver-824-database-engine-error.md)。 
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 将 PAGE_VERIFY 数据库选项设置为 CHECKSUM。 使用 PAGE_VERIFY CHECKSUM 数据库选项能够以最可靠的方式检测由系统 I/O 路径引起的数据库一致性问题。
  
## <a name="for-more-information"></a>有关详细信息  
 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
