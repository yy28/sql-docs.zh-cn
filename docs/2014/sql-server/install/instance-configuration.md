---
title: 实例配置 |Microsoft Docs
ms.custom: ''
ms.date: 2016-05-04
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9177aa0abe0a5f2a3746486c5cf71163bcd1e1be
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791293"
---
# <a name="instance-configuration"></a>实例配置
  使用 **安装向导的** “实例配置” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 页面可指定是创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的默认实例还是其命名实例。 如果尚未安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，则除非您指定命名实例，否则将创建默认实例。  
  
 每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例都由一组具有排列规则及其他选项特定设置的非重复的服务组成。 目录结构、注册表结构和服务名称都反映在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中创建的实例名称和特定实例 ID。  
  
 实例是默认实例或命名实例。 默认实例名为 MSSQLSERVER。 不需要客户端指定实例名称便可进行连接。 命名实例在安装过程中由用户决定。 您可以将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作为命名实例安装，无需先安装默认实例。 不论版本如何，一次均只能安装一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]默认实例。  
  
 **警报 ！** 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep，您可以在 **“实例配置”** 页上完成已准备实例时指定实例名称。 如果在计算机上没有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的现有默认实例，您可以选择将正在完成的已准备实例配置为默认实例。  
  
## <a name="multiple-instances"></a>多实例  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持在单个服务器或处理器上存在多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，但只能有一个实例为默认实例。 所有其他实例必须为命名实例。 一台计算机可同时运行多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，每个实例独立于其他实例运行。  
  
 有关详细信息，请参阅 [Maximum Capacity Specifications for SQL Server](../maximum-capacity-specifications-for-sql-server.md)。  
  
## <a name="options"></a>选项  
 仅限故障转移群集实例 - 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集网络名称。 此名称可用来在网络上标识故障转移群集实例。  
  
 默认实例或命名实例 - 当决定是安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例还是命名实例时，请考虑以下信息：  
  
-   如果计划在数据库服务器上安装单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，则该实例应为默认实例。  
  
-   如果您打算在同一台计算机上安装多个实例，请使用命名实例。 一台服务器只能承载一个默认实例。  
  
-   任何安装 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 的应用程序都应将其作为命名实例安装。 当同一台计算机中安装多个应用程序时，这样可以最大程度地减少冲突。  
  
 **默认实例**  
 选择该选项可安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例。 一台计算机只能承载一个默认实例；所有其他实例必须是命名实例。 但是，如果您已经安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例，则可以向同一台计算机添加 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的默认实例。  
  
 **命名实例**  
 选择该选项可创建新的命名实例。 当对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例进行命名时，请注意以下几点：  
  
-   实例名不区分大小写。  
  
-   实例名不能以下划线 (_) 开始或结束。  
  
-   实例名称不能包含词语“Default”或其他保留关键字。 如果在实例名中使用了保留关键字，将发生安装错误。 有关详细信息，请参阅[保留关键字 (Transact-SQL) ](/sql/t-sql/language-elements/reserved-keywords-transact-sql)。  
  
-   如果为实例名称指定 MSSQLServer，将创建默认实例。  
  
-   [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] 安装始终安装为命名实例“PowerPivot”。 您不能为此功能角色指定不同的实例名称。  
  
-   实例名限制为 16 个字符。  
  
-   实例名中的第一个字符必须是字母。 可接受的字母为 Unicode 标准 2.0 定义的那些字母。 这些字母包括拉丁字符 a-z、A-Z 和其他语言中的字母字符。  
  
-   后续字符可以是 Unicode 标准 2.0 定义的字母、源于基本拉丁语或其他国家/地区书写符号的十进制数字、美元符号 ($) 或者下划线 (_)。  
  
-   实例名称中不允许含有空格或其他特殊字符， 也不允许存在反斜杠 (\\)、逗号 (,)、冒号 (:)、分号 (;)、单引号 (')、& 号 (&)、连字号 (-) 和 at 符 (@)。  
  
-   **只有在当前 Windows 代码页中有效的字符可在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的名称。如果使用的不受支持的 Unicode 字符，则将发生安装错误。**  
  
 **检测到的实例和功能**  
 查看正在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的计算机中安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例和组件的列表。  
  
 **实例 ID** - 默认情况下，实例名称用作实例 ID。 这用于标识 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的安装目录和注册表项。 默认实例和命名实例的默认方式都是如此。 对于默认实例，实例名称和实例 ID 为 MSSQLSERVER。 若要使用非默认的实例 ID，请在 **实例 ID** 字段中指定它。  
  
> [!IMPORTANT]  
>  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep，在此页上显示的实例 ID 是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 过程的准备映像步骤中指定的实例 ID。 在完成映像步骤中，您将无法指定不同的实例 ID。  
  
> [!NOTE]  
>  不支持以下划线 (_) 开头或者包含数字符号 (#) 或美元符号 ($) 的实例 ID。  
  
 有关目录、文件位置和实例 ID 命名的详细信息，请参阅 [默认和已命名的 SQL Server 实例的文件位置](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的给定实例的所有组件作为一个单元进行管理。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升级都将应用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的每个组件。  
  
 共用同一实例名称的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件都必须满足以下条件：  
  
-   版本相同  
  
-   版本类别相同  
  
-   语言设置相同  
  
-   聚集状态相同  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不能识别群集。  
  
-   操作系统相同  
  
  
