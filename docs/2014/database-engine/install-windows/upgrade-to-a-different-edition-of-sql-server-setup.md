---
title: 升级到另一版本的 SQL Server 2014 （安装程序） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 31d16820-d126-4c57-82cc-27701e4091bc
caps.latest.revision: 26
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d88903151c3557ec48b9457a50d4a257075eb04
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37182854"
---
# <a name="upgrade-to-a-different-edition-of-sql-server-2014-setup"></a>升级到 SQL Server 2014 的另一版本（安装）
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序支持在各种版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 间进行版本升级。 有关支持的版本升级路径的信息，请参阅 [支持的版本升级](supported-version-and-edition-upgrades.md)。 在开始对 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]实例执行版本升级前，请查看以下主题：  
  
-   [SQL Server 2014 各个版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
-   [SQL Server 2014 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)  
  
-   [按 SQL Server 版本划分的计算能力限制](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
-   [安装 SQL Server 2014 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
> [!NOTE]  
>  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：** 对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 群集中的一个节点运行版本升级就足够了。 此节点可以是活动节点或被动节点，并且在版本升级过程中引擎不使资源脱机。 版本升级后需要重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例或故障转移到其他节点。  
  
## <a name="prerequisites"></a>必要條件  
 对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取权限的域帐户。  
  
> [!IMPORTANT]  
>  为了激活对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本进行的更改，必须重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 这将导致应用程序在服务脱机时关闭。  
  
## <a name="procedure"></a>过程  
  
#### <a name="to-upgrade-to-a-different-edition-of-includesscurrentincludessscurrent-mdmd"></a>升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的另一版本  
  
1.  插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装介质， 在根文件夹中，双击 setup.exe 或者从配置工具中启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装中心。 若要从网络共享进行安装，请找到共享中的根文件夹，然后双击 Setup.exe。  
  
2.  若要将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的现有实例升级到另一版本，请在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装中心中单击 **“维护”**，然后选择 **“版本升级”**。  
  
3.  如果需要使用安装程序支持文件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将安装它们。 如果安装程序指示您重新启动计算机，请在继续操作之前重新启动。  
  
4.  系统配置检查器将在您的计算机上运行发现操作。 若要继续，请单击 **“确定”**。  
  
5.  在“产品密钥”页上，选择相应的单选按钮，这些按钮指示您是升级到免费版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，还是您拥有该产品生产版本的 PID 密钥。 有关详细信息，请参阅[各版本和 SQL Server 2014 的组件](../../sql-server/editions-and-components-of-sql-server-2016.md)并[Supported Version and Edition Upgrades](supported-version-and-edition-upgrades.md)。  
  
6.  在“许可条款”页上阅读许可协议，然后选中相应的复选框以接受许可条款和条件。 若要继续，请单击 **“下一步”**。 若要结束安装程序，请单击 **“取消”**。  
  
7.  在“选择实例”页上指定要升级的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
8.  在版本升级操作开始之前，“版本升级规则”页会验证您的计算机配置。  
  
9. “准备升级版本”页显示您在安装过程中指定的安装选项的树视图。 若要继续，请单击 **“升级”**。  
  
10. 在版本升级过程中，需要重新启动服务以便接受新设置。 版本升级完成后，“完成”页会提供指向版本升级摘要日志文件的链接。 若要关闭该向导，请单击 **“关闭”**。  
  
11. “完成”页会提供指向安装日志文件摘要以及其他重要说明的链接。  
  
12. 如果安装程序指示您重新启动计算机，请立即重新启动。 安装完成后，请务必阅读来自安装向导的消息。 有关安装程序日志文件的信息，请参阅 [查看和阅读 SQL Server 安装程序日志文件](view-and-read-sql-server-setup-log-files.md)。  
  
13. 如果是从 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]进行的升级，则必须执行以下附加步骤才能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的升级实例：  
  
    -   在 Windows SCM 中启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务。  
  
    -   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务帐户。  
  
 如果是从 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]升级，除了执行上面的步骤外，您可能还需要执行下列操作：  
  
-   升级之后，在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中设置的用户将保持其原有的设置。 具体而言，BUILTIN\Users 组将保持其原有的设置。 可以根据需要禁用、删除或重新设置这些帐户。 有关详细信息，请参阅 [配置 Windows 服务帐户和权限](../configure-windows/configure-windows-service-accounts-and-permissions.md)预览版本升级问题的解答。  
  
-   升级之后，tempdb 和 model 系统数据库的大小和恢复模式保持不变。 可以根据需要重新配置这些设置。 有关详细信息，请参阅[备份和还原系统数据库 (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。  
  
-   升级之后，模板数据库保留在计算机上。  
  
## <a name="see-also"></a>请参阅  
 [升级到 SQL Server 2014](upgrade-sql-server.md)   
 [后向兼容性](../../getting-started/backward-compatibility.md)  
  
  
