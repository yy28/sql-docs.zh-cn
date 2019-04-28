---
title: 服务器配置选项 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- surface area configuration [SQL Server], sp_configure
- configuration options [SQL Server], when take effect
- server management [SQL Server], configuration options
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], configuring
- configuration options [SQL Server], setting
- options [SQL Server], configuration
- RECONFIGURE statement
- performance [SQL Server], servers
- configuration options [SQL Server]
- RECONFIGURE WITH OVERRIDE statement
- SQL Server, configuring
- sp_configure
- stored procedures [SQL Server], configuration options
- server configuration [SQL Server]
- administering SQL Server, configuration options
ms.assetid: 9f38eba6-39b1-4f1d-ba24-ee4f7e2bc969
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 645aee1374f7dbf3c290500bb35ca47115983670
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62809565"
---
# <a name="server-configuration-options-sql-server"></a>服务器配置选项 (SQL Server)
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sp_configure 系统存储过程通过配置选项来管理和优化 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 资源。 大多数常用的服务器配置选项可以通过 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]来使用；而所有配置选项都可通过 sp_configure 来访问。 在设置这些选项之前应该认真考虑这些选项对系统的影响。 有关详细信息，请参阅[查看或更改服务器属性 (SQL Server)](view-or-change-server-properties-sql-server.md)。  
  
> [!IMPORTANT]  
>  高级选项只能由有经验的数据库管理员或认证的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术人员更改。  
  
## <a name="categories-of-configuration-options"></a>配置选项的分类  
 配置选项在下面两种情况下生效：  
  
-   在设置选项并发出 RECONFIGURE（在某些情况下为 RECONFIGURE WITH OVERRIDE）语句之后立即生效。  
  
     -或-  
  
-   执行以上操作并重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例之后生效。  
  
 需要重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的选项最初只在 value 列中显示更改后的值。 在重新启动后，新值将出现在 value 列和 value_in_use 列中。  
  
 但有些选项需要在重新启动服务器后，新的配置值才能生效。 如果设置了新值并在没有重新启动服务器的情况下运行 sp_configure，则新值将出现在配置选项的 value 列中，而不是出现在 value_in_use 列中。 重新启动服务器之后，新值将出现在 value_in_use 列中。  
  
 自配置选项是指 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 根据系统需要进行调整的选项。 大多数情况下，这使您无需手动设置值。 这方面的例子包括 min server memory、max server memory 和 user connections 选项。  
  
## <a name="configuration-options-table"></a>配置选项表  
 下表列出了所有可用的配置选项、可能的设置范围及其默认值。 配置选项按以下字母代码标记：  
  
-   A = 高级选项，仅允许有经验的数据库管理员或经过认证的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术人员进行更改，并且需要将 show advanced options 设置为 1。  
  
-   RR = 需要重新启动[!INCLUDE[ssDE](../../includes/ssde-md.md)]的选项。  
  
-   SC = 自配置选项。  
  
    |配置选项|最小值|最大值|默认|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[访问检查缓存桶计数](access-check-cache-server-configuration-options.md) (A)|0|16384|0|  
    |[访问检查缓存配额](access-check-cache-server-configuration-options.md) (A)|0|2147483647|0|  
    |[即席分布式查询](ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|1|0|  
    |[affinity I/O mask](affinity-input-output-mask-server-configuration-option.md) （A，RR）|-2147483648|2147483647|0|  
    |[affinity64 I/O mask](affinity64-input-output-mask-server-configuration-option.md) （A，仅适用于 64 位版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）|-2147483648|2147483647|0|  
    |[affinity mask](affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 mask](affinity64-mask-server-configuration-option.md) （A，RR），仅适用于 64 位版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[代理 XP](agent-xps-server-configuration-option.md) (A)|0|1|0<br /><br /> （当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理启动时，更改为 1。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理设置为在安装过程中自动启动，则默认值为 0。）|  
    |[允许更新](allow-updates-server-configuration-option.md) （已过时。 请勿使用。 将在重新配置期间导致错误。）|0|1|0|  
    |[备份校验和默认值](../backup-checksum-default.md)|0|1|0|  
    |[backup compression default](view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|1|0|  
    |[blocked process threshold](blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[c2 审核模式](c2-audit-mode-server-configuration-option.md) （A，RR）|0|1|0|  
    |[clr enabled](clr-enabled-server-configuration-option.md)|0|1|0|  
    |[common criteria compliance enabled](common-criteria-compliance-enabled-server-configuration-option.md) （A，RR）|0|1|0|  
    |[contained database authentication](contained-database-authentication-server-configuration-option.md)|0||0|  
    |[并行的开销阈值](configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](cross-db-ownership-chaining-server-configuration-option.md)|0|1|0|  
    |[cursor threshold](configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Database Mail XPs](database-mail-xps-server-configuration-option.md) (A)|0|1|0|  
    |[default full-text language](configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|2052|  
    |[default language](configure-the-default-language-server-configuration-option.md)|0|9999|0|  
    |[default trace enabled](default-trace-enabled-server-configuration-option.md) (A)|0|1|1|  
    |[disallow results from triggers](disallow-results-from-triggers-server-configuration-option.md) (A)|0|1|0|  
    |[EKM provider enabled](ekm-provider-enabled-server-configuration-option.md)|0|1|0|  
    |[filestream_access_level](filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[填充因子](configure-the-fill-factor-server-configuration-option.md) （A，RR）|0|100|0|  
    |ft crawl bandwidth (max)，请参阅 [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft crawl bandwidth (min)，请参阅 [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |ft notify bandwidth (max)，请参阅 [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft notify bandwidth (min)，请参阅 [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |[index create memory](configure-the-index-create-memory-server-configuration-option.md) （A，SC）|704|2147483647|0|  
    |[in-doubt xact resolution](in-doubt-xact-resolution-server-configuration-option.md) (A)|0|2|0|  
    |[lightweight pooling](lightweight-pooling-server-configuration-option.md) （A，RR）|0|1|0|  
    |[locks](configure-the-locks-server-configuration-option.md) （A，RR，SC）|5000|2147483647|0|  
    |[max degree of parallelism](configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[max full-text crawl range](max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[max server memory](server-memory-server-configuration-options.md) （A，SC）|16|2147483647|2147483647|  
    |[max text repl size](configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[max worker threads](configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> （对于 32 位 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，建议最大为 1024；对于 64 位 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，建议最大为 2048。）|0<br /><br /> 归零操作会根据处理器的数量自动配置最大工作线程数，可以使用公式 (256+(\<处理器数> -4) * 8) 来计算 32 位 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的线程数，64 位 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的线程数为 32 位的 2 倍。|  
    |[media retention](configure-the-media-retention-server-configuration-option.md) （A，RR）|0|365|0|  
    |[min memory per query](configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[min server memory](server-memory-server-configuration-options.md) （A，SC）|0|2147483647|0|  
    |[嵌套触发器](configure-the-nested-triggers-server-configuration-option.md)|0|1|1|  
    |[network packet size](configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Ole Automation Procedures](ole-automation-procedures-server-configuration-option.md) (A)|0|1|0|  
    |[open objects](open-objects-server-configuration-option.md) （A，RR，已过时）|0|2147483647|0|  
    |[针对即席工作负荷进行优化](optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|1|0|  
    |[PH_timeout](ph-timeout-server-configuration-option.md) (A)|1|3600|60|  
    |[precompute rank](precompute-rank-server-configuration-option.md) (A)|0|1|0|  
    |[priority boost](configure-the-priority-boost-server-configuration-option.md) （A，RR）|0|1|0|  
    |[query governor cost limit](configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[查询等待](configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[恢复间隔](configure-the-recovery-interval-server-configuration-option.md) （A，SC）|0|32767|0|  
    |[远程访问](configure-the-remote-access-server-configuration-option.md) (RR)|0|1|1|  
    |[remote admin connections](remote-admin-connections-server-configuration-option.md)|0|1|0|  
    |[remote login timeout](configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[remote proc trans](configure-the-remote-proc-trans-server-configuration-option.md)|0|1|0|  
    |[remote query timeout](configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|600|  
    |[Replication XPs 选项](replication-xps-server-configuration-option.md) (A)|0|1|0|  
    |[scan for startup procs](configure-the-scan-for-startup-procs-server-configuration-option.md) （A，RR）|0|1|0|  
    |[server trigger recursion](server-trigger-recursion-server-configuration-option.md)|0|1|1|  
    |[set working set size](set-working-set-size-server-configuration-option.md) （A，RR，已过时）|0|1|0|  
    |[show advanced options](show-advanced-options-server-configuration-option.md)|0|1|0|  
    |[SMO 和 DMO XP](smo-and-dmo-xps-server-configuration-option.md) (A)|0|1|1|  
    |[transform noise words](transform-noise-words-server-configuration-option.md) (A)|0|1|0|  
    |[两位数年份截止](configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9999|2049|  
    |[user connections](configure-the-user-connections-server-configuration-option.md) （A，RR，SC）|0|32767|0|  
    |[user options](configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](xp-cmdshell-server-configuration-option.md) (A)|0|1|0|  
  
## <a name="see-also"></a>请参阅  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
