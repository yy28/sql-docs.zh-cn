---
title: 查看和读取 SQL Server 安装程序日志文件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying log files
- Setup [SQL Server], logs
- installation log files [SQL Server]
- installing SQL Server, logs
- errors [SQL Server], Setup
- logs [SQL Server], Setup
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d6a81258e87bf2422f3ae5a55afc5eb6429856b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774319"
---
# <a name="view-and-read-sql-server-setup-log-files"></a>查看和阅读 SQL Server 安装程序日志文件
  每次执行安装程序中创建的日志文件与新的时间戳的日志文件夹位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\。 带有时间戳的日志文件夹的名称格式为 YYYYMMDD_hhmmss。 在无人参与模式下运行安装程序时，将在 % temp%\sqlsetup*.log 中创建日志。 日志文件夹中的所有文件将归档到各自日志文件夹的 Log\*.cab 文件中。  
  
 一个典型的安装请求将经历以下三个执行阶段：  
  
1.  全局规则文本  
  
2.  组件更新  
  
3.  用户请求的操作  
  
 在每个阶段中，安装程序都生成详细信息日志和摘要日志，并根据需要创建其他日志。 在每次执行用户请求的安装操作时安装程序至少会被调用三次。  
  
 数据存储文件包含安装过程所跟踪的所有配置对象状态的快照，对于纠正配置错误来说非常有用。 XML 文件转储是为每个执行阶段的数据存储对象创建的。 它们保存在带有时间戳的日志文件夹下其自己的日志子文件夹中，如下所示：  
  
-   Datastore_GlobalRules  
  
-   Datastore_ComponentUpdated  
  
-   Datastore  
  
 以下部分介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序日志文件。  
  
## <a name="summary-text"></a>摘要文本  
  
### <a name="overview"></a>概述  
 此文件显示在安装过程中检测到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件、操作系统环境、命令行参数值（如果已指定），以及执行的每个 MSI/MSP 的总体状态。  
  
 本日志归纳为以下部分：  
  
-   执行的总体摘要  
  
-   运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的计算机的属性和配置  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 产品功能  
  
-   安装版本和安装包属性的说明  
  
-   安装过程中提供的运行时输入设置  
  
-   配置文件的位置  
  
-   执行结果的详细信息  
  
-   全局规则  
  
-   特定于安装方案的规则  
  
-   失败的规则  
  
-   规则报表文件的位置  
  
### <a name="location"></a>Location  
 位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\。  
  
 若要找到摘要文本文件中的错误，请使用“error”或“failed”关键字搜索该文件。  
  
## <a name="summaryengine-baseyyyymmddhhmmsstxt"></a>Summary_engine-base_YYYYMMDD_HHMMss.txt  
  
### <a name="overview"></a>概述  
 summary_engine 基本文件类似于摘要文件，是在主工作流中生成的。  
  
### <a name="location"></a>Location  
 位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\。  
  
## <a name="summaryengine-baseyyyymmddhhmmsscomponentupdatetxt"></a>Summary_engine-base_YYYYMMDD_HHMMss_ComponentUpdate.txt  
  
### <a name="overview"></a>概述  
 组件更新摘要日志文件类似于摘要文件，是在组件更新工作流中生成的。  
  
### <a name="location"></a>Location  
 位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\。  
  
## <a name="summaryengine-baseversionnumbermmddhhmmssglobalrulestxt"></a>Summary_engine-base_\<VersionNumber>MMDD_HHMMss_GlobalRules.txt  
  
### <a name="overview"></a>概述  
 全局规则摘要日志文件类似于摘要文件，是在全局规则工作流中生成的。  
  
### <a name="location"></a>Location  
 位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\。  
  
## <a name="detailtxt"></a>Detail.txt  
  
### <a name="overview"></a>概述  
 Detail.txt 是针对主工作流（如安装或升级）生成的，它提供有关执行的详细信息。 文件中的日志基于调用每个安装操作的时间而生成，并且显示操作的执行顺序以及其依赖项。  
  
### <a name="location"></a>Location  
 位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup  
  
 Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt。  
  
 如果在安装过程中发生错误，则将异常或错误记录在该文件的末尾。 若要查找该文件中的错误，请首先检查文件末尾，然后在文件中搜索“错误”或“异常”关键字。  
  
## <a name="detailcomponentupdatetxt"></a>Detail_ComponentUpdate.txt  
  
### <a name="overview"></a>概述  
 Detail_ComponentUpdate.txt 文件是针对组件更新工作流而生成的，它类似于 Detail.txt。  
  
### <a name="location"></a>Location  
 位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\。  
  
## <a name="detailglobalrulestxt"></a>Detail_GlobalRules.txt  
  
### <a name="overview"></a>概述  
 Detail_GlobalRules.txt 是针对全局规则执行而生成的，它类似于 Detail.txt。  
  
### <a name="location"></a>Location  
 位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\。  
  
## <a name="msi-log-files"></a>MSI 日志文件  
  
### <a name="overview"></a>概述  
 MSI 日志文件提供安装包进程的详细信息。 它们是在安装指定的包的过程中由 MSIEXEC 生成的。  
  
 MSI 日志文件的类型：  
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log  
  
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log  
  
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### <a name="location"></a>Location  
 MSI 日志文件位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\< 名称\>。 日志。  
  
 该文件的末尾是有关执行的摘要，其中包括成功状态或失败状态以及属性。 若要找到 MSI 文件中的错误，请搜索“value 3”，通常可找到的错误与此字符串接近。  
  
## <a name="configurationfileini"></a>ConfigurationFile.ini  
  
### <a name="overview"></a>概述  
 本配置文件包含安装过程中提供的输入设置。 该文件可用于在无需手动输入设置的情况下重新启动安装。 但是，帐户的密码、PID 和某些参数不保存在该配置文件中。 可以将这些设置添加到该文件中，也可通过使用命令行或安装程序用户界面提供这些设置。 有关详细信息，请参阅[使用安装 SQL Server 2014 配置文件](install-sql-server-using-a-configuration-file.md)。  
  
### <a name="location"></a>Location  
 位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\。  
  
## <a name="systemconfigurationcheckreporthtm"></a>SystemConfigurationCheck_Report.htm  
  
### <a name="overview"></a>概述  
 系统配置检查报表包含有关每个执行规则的简短说明，以及执行状态。  
  
### <a name="location"></a>Location  
 位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\。  
  
## <a name="see-also"></a>请参阅  
 [安装操作指南主题](../../sql-server/install/installation-how-to-topics.md)   
 [安装 SQL Server 2014](install-sql-server.md)  
  
  
