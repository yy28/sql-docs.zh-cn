---
title: "配置 SQL Server 以向 Microsoft 发送反馈 | Microsoft Docs"
description: 
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 07/12/2017
ms.topic: article
ms.prod: sql-server-2016
ms.technology: database-engine
ms.assetid: 
ms.translationtype: HT
ms.sourcegitcommit: dd279b20fdf0f42d4b44843244aeaf6f19f04718
ms.openlocfilehash: de638f50e6c11633859e7cdc3c6ddb208fe64f00
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---

# <a name="configure-sql-server-to-send-feedback-to-microsoft"></a>配置 SQL Server 以向 Microsoft 发送反馈

## <a name="summary"></a>摘要
默认情况下，Microsoft SQL Server 收集有关其客户如何使用应用程序的信息。 具体来说，SQL Server 收集有关安装体验、使用情况和性能的信息。 此信息有助于 Microsoft 改进产品以更好地满足客户需求。 例如，Microsoft 收集有关客户遇到的错误代码类型信息，这样我们就可以修复相关 bug，改进关于如何使用 SQL Server 的文档，并确定是否应将功能添加到产品中以更好地为客户服务。

具体而言，Microsoft 不会通过这种机制发送以下任何类型的信息：
- 用户表中的任何值
- 任何登录凭据或其他身份验证信息
- 个人身份信息 (PII)

以下示例场景包括有助于改进产品的功能使用情况信息。

SQL Server 2017 支持列存储索引，以实现快速分析方案。 列存储索引将新插入数据的传统“B 树”索引结构与面向列的特殊压缩结构相结合，以压缩数据并加快查询执行速度。 该产品使用探索性方法在后台将数据从 B 树结构迁移到压缩结构，可加快后续获取查询结果的过程。

如果后台操作未与插入数据的速度保持一致，则查询性能可能比预期要慢。 为了改进产品，Microsoft 收集有关 SQL Server 与自动数据压缩过程同步情况的信息。 产品团队使用此信息来微调执行压缩的代码的频率和并行结构。 此查询偶尔运行以收集此信息，以便我们 (Microsoft) 可以评估数据移动速度。 这有助于我们优化产品探索方法。  

```sql
SELECT object_id, type_desc, data_space_id, db_id() AS database_id FROM sys.indexes WITH(nolock) WHERE type = 5 or type = 6 
```

```sql
SELECT cntr_value as merge_policy_evaluation
FROM sys.dm_os_performance_counters WITH(nolock)
WHERE object_name LIKE '%columnstore%' 
AND counter_name ='Total Merge Policy Evaluations' 
AND instance_name = '_Total'
```

请注意，此过程专注于为客户提供价值的必要机制。 产品团队不会查看索引中的数据，也不会将该数据发送给 Microsoft。 SQL Server 2017 始终收集和发送从安装过程开始的安装体验相关信息，方便我们快速查找并修复客户遇到的任何安装问题。 通过以下机制可将 SQL Server 2017 配置为不（基于每个服务器实例）向 Microsoft 发送信息：
- 通过使用错误和使用情况报告应用程序
- 通过在服务器上设置注册表子项

对于 Linux 上的 SQL Server，请参阅 [Linux 上的 SQL Server 客户反馈](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-customer-feedback.md)

> [!NOTE]
> 只能在付费版本的 SQL Server 中禁用向 Microsoft 发送信息的功能。

## <a name="error-and-usage-reporting-application"></a>错误和使用情况报告应用程序 

安装后，可以通过错误和使用情况报告应用程序更改 SQL Server 组件和实例的使用情况数据收集设置。 可将此应用程序作为 SQL Server 安装的一部分。 此工具可使每个 SQL Server 实例配置其自己的使用情况数据设置。

> [!NOTE]
> 错误和使用情况报告应用程序在 SQL Server 的“配置工具”下列出。 使用此工具，你可以通过与在 SQL Server 2017 中相同的方式管理错误报告和使用情况反馈收集的偏好设置。 错误报告不同于使用情况反馈收集，因此可以独立于使用情况反馈收集进行启用或禁用。 错误报告收集发送到 Microsoft 的故障转储，其中可能包含隐私声明中所述的敏感信息。

要启动 SQL Server 错误和使用情况报告，请单击或点击“启动”，然后在搜索框中搜索“错误”。 将显示 SQL Server 错误和使用情况报告项。 启动该工具后，可以管理针对计算机上安装的实例和组件收集的使用情况反馈和严重错误。

对于付费版本，请使用“使用情况报告”复选框来管理向 Microsoft 发送使用情况反馈功能。

对于付费或免费版本，请使用“错误报告”复选框来管理向 Microsoft 发送有关严重错误和故障转储反馈的功能。

## <a name="set-registry-subkeys-on-the-server"></a>在服务器上设置注册表子项

企业客户可以配置组策略设置，以选择加入或退出使用情况数据收集。 这可通过配置基于注册表的策略完成。 相关注册表子项和设置如下所示：

- 对于 SQL Server 实例功能：
    
    子项 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE
    
    注册表项名称 = CustomerFeedback
    
    条目类型 DWORD：0 表示选择退出；1 表示选择加入
    
    {InstanceID} 是指实例类型和实例，如以下示例所示：

    - MSSQL14.CANBERRA 是指 SQL Server 2017 数据库引擎，“CANBERRA”指实例名称
    - MSAS14.CANBERRA 是指 SQL Server 2017 Analysis Services，“CANBERRA”指实例名称
    - MSRS14.CANBERRA 是指 SQL Server 2017 Reporting Services，“CANBERRA”指实例名称

- 对于所有共享功能：
    
    子项 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Major Version}
    
    注册表项名称 = CustomerFeedback
    
    条目类型 DWORD：0 表示选择退出；1 表示选择加入

> [!NOTE]
> {Major Version} 是指 SQL Server 的版本，例如，140 表示 SQL Server 2017

- 对于 SQL Server Management Studio：
  
    子项 = HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\140

    注册表项名称 = CustomerFeedback

    条目类型 DWORD：0 表示选择退出；1 表示选择加入

此外，若要在 Visual Studio 级别禁用使用情况和错误报告，请设置以下注册表子项和设置：

-    子项 = HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\Telemetry

-    注册表项名称 = TurnOffSwitch

-    条目类型 DWORD：0 表示选择退出；1 表示选择加入
 
这些注册表子项上基于注册表的组策略适用于 SQL Server 2017 使用情况数据收集。

## <a name="set-registry-subkeys-for-crash-dump-collection"></a>设置故障转储收集的注册表子项

与 SQL Server 早期版本的行为类似，SQL Server 2017 Enterprise 客户可以在服务器上配置组策略设置，以选择加入或退出故障转储收集。 这可通过配置基于注册表的策略完成。 相关注册表子项和设置如下所示： 

- 对于 SQL Server 实例功能：

    子项 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE

    注册表项名称 = EnableErrorReporting

    条目类型 DWORD：0 表示选择退出；1 表示选择加入
 
    {InstanceID} 是指实例类型和实例，如以下示例所示： 

    - MSSQL14.CANBERRA 是指 SQL Server 2017 数据库引擎，“CANBERRA”指实例名称
    - MSAS14.CANBERRA 是指 SQL Server 2017 Analysis Services，“CANBERRA”指实例名称
    - MSRS14.CANBERRA 是指 SQL Server 2017 Reporting Services，“CANBERRA”指实例名称
 

- 对于所有共享功能：
    
    子项 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Major Version}

    注册表项名称 = EnableErrorReporting

    条目类型 DWORD：0 表示选择退出；1 表示选择加入

> [!NOTE]
> {Major Version} 是指 SQL Server 的版本。 例如，“140”是指 SQL Server 2017。

这些注册表子项上基于注册表的组策略适用于 SQL Server 2017 故障转储收集。 

## <a name="crash-dump-collection-for-ssms"></a>SSMS 的故障转储收集
SSMS 不会收集其自身的故障转储。 与 SSMS 相关的任何故障转储都作为 Windows 错误报告的一部分进行收集。

启用或禁用此功能的过程取决于操作系统版本。 要启用或禁用该功能，请按照 Windows 版本相应文章中的步骤操作。
 
- Windows Server 2016 和 Windows 10

    [在组织中配置 Windows 遥测](https://technet.microsoft.com/en-us/itpro/windows/manage/configure-windows-telemetry-in-your-organization)
- Windows Server 2008 R2 和 Windows 7

    [WER 设置](https://msdn.microsoft.com/en-us/library/windows/desktop/bb513638(v=vs.85).aspx)
 
## <a name="feedback-for-analysis-services"></a>对于 Analysis Services 的反馈

在安装过程中，SQL Server 2016 Analysis Services 向 Analysis Services 实例添加一个特殊帐户。 此帐户是 Analysis Services 服务器管理员角色的成员。 该帐户用于收集来自 Analysis Services 实例的反馈信息。  

可以将服务配置为不发送使用情况数据，如“在服务器上设置注册表子项”部分所述。 但是，执行此操作不会删除服务帐户。 
 
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
