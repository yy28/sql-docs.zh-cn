---
title: 使用基于策略的管理来监视和强制执行最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 61bb69d47ce608762adbfd211470868ccae4a121
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43810783"
---
# <a name="monitor-and-enforce-best-practices-by-using-policy-based-management"></a>使用基于策略的管理来监视和强制执行最佳实践
  基于策略的管理允许您监视的最佳实践[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供一组可以作为最佳实践策略导入的策略文件，然后针对包含实例、实例对象、数据库或数据库对象的目标集评估策略。 您可以手动评估策略，将策略设置为根据计划评估目标集，或者将策略设置为根据事件评估目标集。 有关基于策略的管理的详细信息，请参阅 [使用基于策略的管理来管理服务器](administer-servers-by-using-policy-based-management.md)。  
  
## <a name="policy-and-rules-for-database-engine"></a>用于数据库引擎的策略和规则  
 下表列出了包含的安装的策略[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并包含有关每个策略评估的最佳实践规则的信息。 策略存储为 XML 文件并且必须导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。 有关如何导入策略的详细信息，请参阅 [导入基于策略的管理策略](import-a-policy-based-management-policy.md)。  
  
|策略名称|最佳实践规则|  
|-----------------|------------------------|  
|非对称密钥加密算法|[非对称密钥加密强度](asymmetric-keys-encryption-strength.md)|  
|备份和数据文件位置|[备份文件必须位于与数据库文件分开的设备上](../../database-engine/backup-files-must-be-on-separate-devices-from-the-database-files.md)|  
|数据和日志文件位置|[将数据和日志文件放到不同的驱动器上](place-data-and-log-files-on-separate-drives.md)|  
|数据库自动关闭|[将 AUTO_CLOSE 数据库选项设置为 OFF](set-the-auto-close-database-option-to-off.md)|  
|数据库自动收缩|[将 AUTO_SHRINK 数据库选项设置为 OFF](set-the-auto-shrink-database-option-to-off.md)|  
|数据库排序规则|[将用户定义的数据库排序规则设置为与 master 和 model 数据库的排序规则一致](../../database-engine/set-collation-user-defined-databases-match-master-model-databases.md)|  
|数据库页验证|[将 PAGE_VERIFY 数据库选项设置为 CHECKSUM](set-the-page-verify-database-option-to-checksum.md)|  
|数据库页状态|[检查包含可疑页的数据库的完整性](check-integrity-of-database-with-suspect-pages.md)|  
|Guest 权限|[对用户数据库的 Guest 权限](guest-permissions-on-user-databases.md)|  
|上次成功备份的日期|[过时的备份](outdated-backup.md)|  
|未授予公共服务器权限|[服务器 public 权限](server-public-permissions.md)|  
|SQL Server 32 位关联掩码重叠|[正确的关联掩码和关联输入的输出掩码重叠](correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|SQL Server 64 位关联掩码重叠|[正确的关联掩码和关联输入的输出掩码重叠](correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|SQL Server 关联掩码|[保留关联掩码默认值](keep-the-affinity-mask-default-value.md)|  
|SQL Server 阻塞的进程阈值|[增加或禁用阻塞的进程阈值](increase-or-disable-blocked-process-threshold.md)|  
|SQL Server 默认跟踪|[默认跟踪日志文件已禁用](default-trace-log-files-disabled.md)|  
|SQL Server 动态锁|[保留锁配置选项默认值](keep-the-locks-configuration-option-default-value.md)|  
|SQL Server 轻型池|[禁用轻型池](disable-lightweight-pooling.md)|  
|SQL Server 登录模式|[选择身份验证模式](../security/choose-an-authentication-mode.md)|  
|SQL Server 最大并行度|[设置最大并行度选项以获取最佳性能](set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|32 位 SQL Server 2000 的 SQL Server 最大工作线程数|[验证最大工作线程数设置](verify-max-worker-threads-setting.md)|  
|64 位 SQL Server 2000 的 SQL Server 最大工作线程数|[验证最大工作线程数设置](verify-max-worker-threads-setting.md)|  
|SQL Server 2005 及更高版本的 SQL Server 最大工作线程数|[验证最大工作线程数设置](verify-max-worker-threads-setting.md)|  
|SQL Server 网络数据包大小|[网络数据包大小不应超过 8060 字节](network-packet-size-should-not-exceed-8060-bytes.md)|  
|SQL Server 密码过期|[SQL Server 登录密码过期](sql-server-login-password-expiration.md)|  
|SQL Server 密码策略|[SQL Server 登录密码强度](sql-server-login-password-strength.md)|  
|用户数据库的对称密钥加密|[用户数据库中的对称密钥](symmetric-keys-on-user-databases.md)|  
|master 数据库的对称密钥|[系统数据库中的对称密钥](symmetric-keys-on-system-databases.md)|  
|系统数据库的对称密钥|[系统数据库中的对称密钥](symmetric-keys-on-system-databases.md)|  
|可信数据库|[可信位](trustworthy-bit.md)|  
|Windows 事件日志中的群集磁盘资源损坏错误|[检测 SCSI 主机适配器问题](detect-scsi-host-adapter-issues.md)|  
|Windows 事件日志中的设备驱动程序控制错误|[设备驱动程序控制错误](device-driver-control-error.md)|  
|Windows 事件日志中的设备未就绪错误|[设备未就绪错误](device-not-ready-error.md)|  
|Windows 事件日志中的失败的 I_O 请求错误|[检测失败的输入的输出请求](detect-failed-input-and-output-requests.md)|  
|Windows 事件日志中的 I_O 延迟警告|[检查磁盘输入和输出子系统是否存在 IO 延迟问题](check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Windows 事件日志中的硬件分页错误期间的 I_O 错误|[Input and Output Error During Hard Page Fault](input-and-output-error-during-hard-page-fault.md)|  
|Windows 事件日志中的读取重试错误|[检查磁盘 I/O 子系统是否存在读取重试问题](check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Windows 事件日志中的存储系统 I_O 超时错误|[存储系统输入输出超时](storage-system-input-output-time-out.md)|  
|Windows 事件日志中的系统故障错误|[意外的系统故障](unexpected-system-failures.md)|  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理方面](working-with-policy-based-management-facets.md)  
  
  
