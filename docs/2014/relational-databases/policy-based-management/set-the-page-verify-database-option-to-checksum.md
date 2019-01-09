---
title: 将 PAGE_VERIFY 数据库选项设置为 CHECKSUM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fe1a48e74503e93199a6e91f8b9aa60c21bb9ee1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52778969"
---
# <a name="set-the-pageverify-database-option-to-checksum"></a>将 PAGE_VERIFY 数据库选项设置为 CHECKSUM
  此规则检查 PAGE_VERIFY 数据库选项是否已设置为 CHECKSUM。 为 PAGE_VERIFY 数据库选项启用 CHECKSUM 后， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 会在向磁盘中写入页面时计算整个页面内容的校验并将该值存储在页头中。 从磁盘中读取页时，将重新计算校验和，并与存储在页头中的校验和值进行比较。 这有助于提供高级别的数据文件完整性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 将 PAGE_VERIFY 数据库选项设置为 CHECKSUM。  
  
## <a name="for-more-information"></a>有关详细信息  
 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
