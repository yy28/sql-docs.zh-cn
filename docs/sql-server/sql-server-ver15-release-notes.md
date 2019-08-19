---
title: SQL Server 2019 发行说明 | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 40040948b56190a3ce94d9484e09a3386548bd31
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028859"
---
# <a name="sql-server-2019-preview-release-notes"></a>SQL Server 2019 预览版发行说明
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 社区技术预览 (CTP) 版本的限制和已知问题。 若要了解相关信息，请参阅：
- [SQL Server 2019 中的新增功能](../sql-server/what-s-new-in-sql-server-ver15.md)

## <a name="ctp-32"></a>CTP 3.2

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2 是 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 的最新公开版本。

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2 仅以评估版形式提供。 不提供任何其他版本。

有关 CTP 版本的支持和许可的完整详情可在安装介质的 `license_Eval.rtf` 中查看。

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

## <a name="documentation"></a>文档

- **问题及其对客户的影响**：SQL Server 2019 (15.x) 的文档受到限制，且其内容包含在 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 文档集中。 文章中特定于 SQL Server 2019 (15.x) 的内容通过“适用于”进行标注  。

- 问题和对客户的影响  ：可按版本筛选 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文档。 使用每个文档页左上角的控件来筛选你的要求。

- **问题及其对客户的影响**：SQL Server 2019 (15.x) 没有可用的脱机内容。

## <a name="hardware-and-software-requirements"></a>硬件和软件要求

- **问题及其对客户的影响**：硬件和软件要求仍在审核中，还不是产品发布的最终版本。

  - **硬件**
    - [Windows - 处理器、内存和操作系统要求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - 系统要求](../linux/sql-server-linux-setup.md#system)
  - **软件**
    - Windows Server 2016 或更高版本。 有关其他要求，请参阅[安装 SQL Server 的要求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2。 可从[下载中心](https://www.microsoft.com/download/details.aspx?id=53344)获取。
    - 对于 Linux，请参阅 [Linux - 受支持的平台](../linux/sql-server-linux-setup.md#supportedplatforms)

## <a name = "release-notes"></a>已排除的支持功能

- **问题及其对客户的影响**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 不包括对以下组件、功能和方案的支持：
  - SQL Server Analysis Services
  - SQL Server Reporting Services
  - Kubernetes 上的 AlwaysOn 可用性组
  - 加速数据库恢复

- **解决方法**：无。 排除适用于所有客户，包括 SQL 早期采用者计划的参与者。

- **适用对象**：所有 CTP 版本

## <a name="updated-compiler"></a>更新后的编译器

- **问题及其对客户的影响**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 是通过更新后的编译器构建的。 CTP 2.1 具有一项已知问题，即浮点和其他转换方案的结果可能因更新后的编译器而返回与先前版本不同的值。 CTP 2.2 内附可确保受影响的方案与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 先前版本返回相同结果的任务。 自 CTP 3.2 版本起，已解决所有历史问题。 请将与 [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] 比较得出的所有结果异常立即报告给 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 团队](https://aka.ms/sqlfeedback)。

- **解决方法**：空值

- **适用对象**：所有 CTP 版本

## <a name="installation-wizard-may-wait-between-eula-pages"></a>安装向导可能会在 EULA 页面之间等待

- **问题及其对客户的影响**：在使用安装向导进行安装期间，该过程可能会在 R 服务的最终用户许可协议 (EULA) 和 Python 的 EULA 之间等待一段时间。

- **解决方法**：等待安装向导继续。 等待的时间可能超过 30 分钟。

- **适用对象**：SQL Server 2019 CTP 3.0

## <a name="utf-8-collations"></a>UTF-8 排序规则

- **问题及其对客户的影响**：支持 UTF-8 的排序规则不能与其他一些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能一起使用。 如果正在使用以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能，则不支持 UTF-8：

  - 内存中 OLTP
  - Polybase 外部表
  - 始终加密

  > [!Note]
  > 目前没有 UI 支持在 Azure Data Studio 或 SQL Server Data Tools (SSDT) 中选择支持 UTF-8 的排序规则。 最新的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] SSMS 版本 18 支持在 UI 中选择支持 UTF-8 的排序规则。
 
- **解决方法**：没有针对 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 的解决方法。

- **适用对象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2、CTP 3.1、CTP 3.0、CTP 2.5、CTP 2.4、CTP 2.3、CTP 2.2、CTP 2.1、CTP 2.0。

## <a name="always-encrypted-with-secure-enclaves"></a>具有安全 Enclave 的 Always Encrypted

- **问题及其对客户的影响**：富计算将挂起性能优化和错误处理增强，默认当前已禁用。

- **解决方法**：若要启用富计算，请运行 `DBCC traceon(127,-1)`。 有关详细信息，请参阅[启用富计算](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

- **适用对象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2、CTP 3.1

## <a name="sql-server-configuration-manager-may-not-start"></a>SQL Server 配置管理器可能无法启动

- **问题及其对客户的影响**：SQL Server 配置管理器 (SSCM) 无法在没有 VCRuntime 140 的计算机上启动。 启动 SSCM 时，用户可能会看到下面的对话框： 

  `
  MMC could not create the snap-in. The snap-in might not have been installed correctly.
  `

- **解决方法**：安装最新的 VC 运行时 2013 (x86)：

  - [Verbose](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)
  - [直接](https://support.microsoft.com/en-us/help/4032938/update-for-visual-c-2013-redistributable-package)

- **适用对象**：[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.1、CTP 3.0、CTP 2.5。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
