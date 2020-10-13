---
title: 最大并行度和基于策略的管理
description: 介绍如何配置策略，以验证 SQL Server 的基于策略的管理的最大并行度值。
ms.custom: seo-lt-2019
ms.date: 07/18/2019
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
ms.openlocfilehash: 6aada496465c642570f9b60a0b1659bbe9ee3db6
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890897"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>设置最大并行度选项以获取最佳性能
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此规则确定最大并行度 (MAXDOP) 选项是否设置为大于 8 的值。 将此选项设置为大于 8 的值通常导致不必要的资源消耗和性能下降。  
  
## <a name="best-practice-recommendations"></a>最佳做法建议  
 最大并行度 (MAXDOP) 配置选项控制并行计划中用于执行查询的处理器数。 此选项确定用于并行执行工作的查询计划运算符的线程数。 必须根据 SQL Server 的安装位置（对称多处理式 (SMP) 计算机、非一致性内存访问 (NUMA) 计算机，或启用了超线程的处理器），适当地配置最大并行度选项。 
 
 配置 MAXDOP 的建议取决于使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 有关特定版本的指导原则，请参阅[配置“最大并行度”服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)，并配置相应的策略来验证最大并行度的值。     
  
## <a name="for-more-information"></a>更多信息  
 [SQL Server 中“最大并行度”配置选项的建议和指南](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)    
 [配置“最大并行度”服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)     
