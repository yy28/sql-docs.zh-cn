---
title: 将 PAGE_VERIFY 数据库选项设置为 CHECKSUM | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
manager: craigg
ms.openlocfilehash: b9c9e3f77ef7d94fa1847bb1df9f846423ec56fc
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512382"
---
# <a name="set-the-pageverify-database-option-to-checksum"></a>将 PAGE_VERIFY 数据库选项设置为 CHECKSUM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此规则检查 PAGE_VERIFY 数据库选项是否已设置为 CHECKSUM。 为 PAGE_VERIFY 数据库选项启用 CHECKSUM 后， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 会在向磁盘中写入页面时计算整个页面内容的校验并将该值存储在页头中。 从磁盘中读取页时，将重新计算校验和，并与存储在页头中的校验和值进行比较。 这有助于提供高级别的数据文件完整性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 将 PAGE_VERIFY 数据库选项设置为 CHECKSUM。  
  
## <a name="for-more-information"></a>有关详细信息  
 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
