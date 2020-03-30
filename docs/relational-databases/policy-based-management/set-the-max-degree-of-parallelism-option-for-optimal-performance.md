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
ms.openlocfilehash: a03a0236c177605bf5041e92ea9c19708d5bc9ae
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "75776376"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>设置最大并行度选项以获取最佳性能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此规则确定最大并行度 (MAXDOP) 选项是否设置为大于 8 的值。 将此选项设置为大于 8 的值通常导致不必要的资源消耗和性能下降。  
  
## <a name="best-practice-recommendations"></a>最佳做法建议  
 最大并行度 (MAXDOP) 配置选项控制并行计划中用于执行查询的处理器数。 此选项确定用于并行执行工作的查询计划运算符的线程数。 必须根据 SQL Server 的安装位置（对称多处理式 (SMP) 计算机、非一致性内存访问 (NUMA) 计算机，或启用了超线程的处理器），适当地配置最大并行度选项。 
 
 配置 MAXDOP 的建议取决于使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 有关特定版本的指导原则，请参阅[配置“最大并行度”服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)，并配置相应的策略来验证最大并行度的值。     
  
## <a name="for-more-information"></a>更多信息  
 [SQL Server 中“最大并行度”配置选项的建议和指南](https://go.microsoft.com/fwlink/?linkid=117786)    
 [配置“最大并行度”服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)     
  
