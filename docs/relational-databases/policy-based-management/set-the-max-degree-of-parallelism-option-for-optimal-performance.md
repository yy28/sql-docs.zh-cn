---
title: 设置最大并行度选项以获取最佳性能 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 10187162bec9286867c56def5c8bc2b4c1ed5382
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51655616"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>设置最大并行度选项以获取最佳性能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此规则确定最大并行度 (MAXDOP) 选项是否设置为大于 8 的值。 将此选项设置为大于 8 的值通常导致不必要的资源消耗和性能下降。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 通过使用 sp_configure 将最大并行度选项设置为 8 或更小。  
  
## <a name="for-more-information"></a>有关详细信息  
 [Microsoft 知识库文章 329204](https://go.microsoft.com/fwlink/?linkid=117786)  
  
 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
