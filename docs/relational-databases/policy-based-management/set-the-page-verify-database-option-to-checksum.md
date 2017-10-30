---
title: "将 PAGE_VERIFY 数据库选项设置为 CHECKSUM | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3bd575c72ea39e3f0b0050bfa508913a652d8023
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="set-the-pageverify-database-option-to-checksum"></a>将 PAGE_VERIFY 数据库选项设置为 CHECKSUM
  此规则检查 PAGE_VERIFY 数据库选项是否已设置为 CHECKSUM。 为 PAGE_VERIFY 数据库选项启用 CHECKSUM 后， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 会在向磁盘中写入页面时计算整个页面内容的校验并将该值存储在页头中。 从磁盘中读取页时，将重新计算校验和，并与存储在页头中的校验和值进行比较。 这有助于提供高级别的数据文件完整性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 将 PAGE_VERIFY 数据库选项设置为 CHECKSUM。  
  
## <a name="for-more-information"></a>有关详细信息  
 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  

