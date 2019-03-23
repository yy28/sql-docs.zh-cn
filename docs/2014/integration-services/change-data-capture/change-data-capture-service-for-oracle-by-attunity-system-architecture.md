---
title: Change Data Capture Service for Oracle by Attunity 系统体系结构 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1db6c737-3c60-4066-a0a3-3611e1c83e4e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 84ac0e6065fa3fb4845e0e3a47ce56816705e80d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389395"
---
# <a name="change-data-capture-service-for-oracle-by-attunity-system-architecture"></a>Change Data Capture Service for Oracle by Attunity 系统体系结构
  Oracle CDC 服务将对一个或多个源 Oracle 数据库中所选表的更改捕获到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC 数据库中。 下面的关系图显示构成 Oracle CDC 服务的各组件。  
  
 ![服务体系结构](../media/service-architecture.gif "Service Architecture")  
  
 下图阐释使用的四个平台。 在许多情况下，这些平台可以重叠，但此关系图表示一个标准用例。 例如，Oracle 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库分别运行在单独的计算机上并且不与 Oracle CDC 服务平台或用于设计 CDC 服务的平台共享是有意义的。 在此图中阐释的平台是：  
  
-   Oracle CDC 服务：这可以是任何受支持的 Windows 计算机，Oracle CDC 服务是安装并运行。 此平台还可以表示 Microsoft 故障转移群集中的某一群集节点（在本文档的后面将论述高可用性配置）。  
  
-   Oracle 数据库中：这可以是任何受支持的版本的 Oracle 数据库在其中运行的计算机。 这包括运行 Windows、Linux 或所安装的 Oracle 数据库版本支持的任何其他操作系统的任何计算机。 请注意，该关系图以复数形式显示此平台，因为单个 Oracle CDC 服务可以从多个源 Oracle 数据库捕获更改。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:这可以是任何计算机的目标[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库 (一种受支持的 SKU 的[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]) 运行。 一个 Oracle CDC 服务支持用于存储更改表和服务配置的一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 目标。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 平台还可以表示 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 的群集实例或使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] AlwaysOn **功能的** 的镜像实例。  
  
-   Oracle CDC 设计器：这可以是任何受支持的 Windows 计算机可以访问源 Oracle 数据库和目标[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库。  
  
 下表描述了在上述四个平台上运行的组件。  
  
|组件/说明|组件由以下项构成：|  
|----------------------------|----------------------------|  
|Oracle CDC 服务：这是一个 Windows 服务更改数据捕获活动发生。|Oracle CDC 实例：句柄，更改数据捕获活动 （没有一个 Oracle CDC 实例，每个源 Oracle 数据库） 的单个源 Oracle 数据库的 Oracle CDC 服务的子进程。<br /><br /> Oracle 日志读取器：读取 Oracle 事务日志使用 Oracle 客户端。<br /><br /> Oracle 客户端：Oracle 即时客户端用于与 Oracle 进行通信。 这是应从 Oracle 获取并在安装 Oracle CDC 服务之前安装的必备组件。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 更改编写器：它将写入提交到捕获的 Oracle 表的更改[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]更改表。 此组件还在目标 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中维护该捕获状态。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ODBC 客户端：适用于 Microsoft 本机客户端[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。 这是应从 Microsoft 获取并在安装 Oracle CDC 服务之前安装的必备组件。|  
|Oracle CDC 服务配置：这是 Microsoft 管理控制台管理单元，创建 Windows 服务，并将其配置设置。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端：使用.NET framework 版本 4 随附的 SQL ADO.NET 客户端。|  
|Oracle 数据库：从选择的表的更改的源 Oracle 数据库捕获。|日志挖掘器：通过其读取 Oracle 事务日志是一种 Oracle 组件。<br /><br /> 事务日志：联机并存档 Oracle 重做日志，Oracle 用于确保数据库可以回滚事务，并从 （在此情况下，Oracle 数据库必须在存档日志模式下操作） 的故障中恢复。|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例：一个[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]其中承载 CDC 数据库的实例。 该实例可以是群集 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例（故障转移群集）或镜像数据库 (AlwaysOn)。|MSXDBCDC 数据库中：数据库位置的 CDC 服务使用此信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]保留实例。 它还保存与每个 CDC 服务处理的 Oracle CDC 实例有关的信息。 该数据库作为 CDC 服务创建进程的一部分创建。<br /><br /> CDC 数据库：存储对源 Oracle 数据库之一进行的更改的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库。 将为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC 启用 CDC 数据库，以便它们具有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC 表和函数，从而轻松地使用来自 Oracle 的更改。|  
|Oracle CDC 设计器：Microsoft 管理控制台管理单元可帮助创建 Oracle CDC 实例。 使用此管理单元可以选择要捕获的表和列，提供 Oracle 连接信息以及管理 CDC 实例的生命周期。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端：使用.NET framework 版本 4 随附的 SQL ADO.NET 客户端。<br /><br /> Oracle 客户端：Oracle 即时客户端用于与 Oracle 进行通信。 这是应从 Oracle 获取并在安装 Oracle CDC 服务之前安装的必备组件。|  
  
 Oracle CDC 服务及其子 Oracle CDC 实例只能与作为客户端的源 Oracle 数据库和目标 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例通信。 它们不主动侦听任何网络和其他协议。 Oracle CDC 服务监视 CDC 数据库中是否有配置更改，并且基于更新的配置更新其操作。  
  
  
