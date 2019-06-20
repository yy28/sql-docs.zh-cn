---
title: 设置最大并行度选项以获取最佳性能 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 794dfea63b193ff79fb5831cb3a4e519d7d5f63e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691387"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>设置最大并行度选项以获取最佳性能
  此规则确定最大并行度 (MAXDOP) 选项是否设置为大于 8 的值。 将此选项设置为大于 8 的值通常导致不必要的资源消耗和性能下降。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 通过使用 sp_configure 将最大并行度选项设置为 8 或更小。  
  
## <a name="for-more-information"></a>有关详细信息  
 [Microsoft 知识库文章 329204](https://go.microsoft.com/fwlink/?linkid=117786)  
  
 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
