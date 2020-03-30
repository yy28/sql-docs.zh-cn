---
title: Oracle 发布服务器性能优化 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], performance tuning
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 31ee9136f4c2b0f0864db0ecd3931e2e45ea4fdb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "67942744"
---
# <a name="performance-tuning-for-oracle-publishers"></a>Oracle 发布服务器性能优化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Oracle 发布体系结构与 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 发布体系结构类似。因此，Oracle 复制性能优化的第一步要求遵循 [Enhance General Replication Performance](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)中提供的一般优化建议。  
  
 此外，还有两个与 Oracle 发布服务器性能有关的选项：  
  
-   指定适当的发布选项：Oracle 或 Oracle 网关。  
  
-   配置事务集作业，使其按照适当的时间间隔处理发布服务器上的更改。  
  
## <a name="specifying-the-appropriate-publishing-option"></a>指定适当的发布选项  
 “Oracle Gateway”选项的性能优于“Oracle Complete”选项；但是，此选项不能用于在多个事务发布中发布同一个表。 一个表最多只能出现在一个事务发布中，但可以出现在任意多个快照发布中。 如果需要在多个事务发布中发布同一个表，请选择“Oracle Complete”选项。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器上标识 Oracle 发布服务器时，请指定此选项。 有关详细信息，请参阅 [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)。  
  
## <a name="configuring-the-transaction-set-job"></a>配置事务集作业  
 对已发布 Oracle 表所做的更改在称为“事务集”的组中处理。 为了确保事务的一致性，每个事务集都作为单一事务在分发数据库上提交。 如果事务集变得过大，则无法作为单一的事务进行有效处理。  
  
 默认情况下，事务集只由日志读取器代理来创建。 在大量更改活动过程中，如果日志读取器代理没有运行，或无法从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器连接到 Oracle 发布服务器，则事务集可能会变得异常大而难以处理。 若要避免此问题，请确保即便在日志读取器代理没有运行或无法连接到 Oracle 发布服务器情况下，仍定期创建事务集。  
  
 可以使用 Xactset 作业（一种通过复制安装的 Oracle 数据库作业）来创建事务集，它所采用的机制与日志读取器代理创建事务集所用的机制相同。 每次该作业运行时，都会创建新的事务集。 日志读取器代理下一次运行时，代理将处理已创建的所有事务集。 如果在处理完所有现有事务集后，仍然存在挂起更改，则日志读取器代理将创建和处理一个或多个额外的事务集。  
  
 若要配置事务集作业，请参阅[为 Oracle 发布服务器配置事务集作业（复制 Transact-SQL 编程）](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)。  
  
## <a name="see-also"></a>另请参阅  
 [配置 Oracle 发布服务器](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 发布概述](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
