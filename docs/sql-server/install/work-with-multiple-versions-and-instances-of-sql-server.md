---
title: "使用 SQL Server 的多个版本和实例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "并发安装 [SQL Server]"
  - "版本 [SQL Server], 多个"
  - "并行安装 [SQL Server]"
  - "多个 SQL Server 组件版本"
  - "安装 SQL Server, 并行安装"
  - "设置 [SQL Server], 并行安装"
  - "64 位版本 [SQL Server]"
  - "32 位版本 [SQL Server]"
  - "版本 [SQL Server], 并行安装"
ms.assetid: 93acefa8-bb41-4ccc-b763-7801f51134e0
caps.latest.revision: 67
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 67
---
# 使用 SQL Server 的多个版本和实例
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持在同一台计算机上存在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的多个实例。 也可以在已安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本的计算机上升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本或安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关支持的升级方案，请参阅[支持的版本和版本升级](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。  
  
## 版本组件和编号  
 下面的概念对于理解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的并行实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的行为十分有用。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的标准产品版本格式为 MM.nn.bbbb.rr，其中每一片断定义为：  
  
 MM - 主版本  
  
 nn - 次版本  
  
 bbbb - 内部版本号  
  
 rr - 内部修订版本号  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个主版本或次版本中，都会增加该版本号，以便与之前的版本区分。 这一对版本的更改出于多种目的。 包括在用户界面中显示版本信息，控制在升级期间替换文件的方式，并且还作为后续版本间在功能上进行区分的机制。  
  
### 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 某些组件由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有已安装版本的所有实例共享。 在同一台计算机上并行安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的不同版本时，这些组件将自动升级到最新的版本。 此类组件通常会在卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的最后的实例时自动卸载。  
  
 示例： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 和 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer。  
  
### 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本在所有实例之间共享某些组件。 如果在升级过程中选择了这些共享的组件，现有组件将升级到最新版本。  
  
 示例： [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书。  
  
### 在次版本之间共享的组件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本共享组件。  
  
 示例：安装程序支持文件。  
  
### 特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件或服务特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。 它们也称为识别实例的组件或服务。 这些组件或服务与承载它们的实例共享相同的版本，并且专用于该实例。  
  
 示例： [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
### 独立于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的组件  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中将安装某些组件，但这些组件独立于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的版本。 它们可在主版本之间共享，或者由所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本共享。  
  
 示例：Microsoft Sync Framework、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact。  
  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 安装的详细信息，请参阅[使用安装向导安装 SQL Server 2016（安装程序）](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)。 有关如何卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 的详细信息，请参阅[卸载现有 SQL Server 实例（安装程序）](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)。  
  
## 并行使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 与其早期版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 可以在已运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本实例的计算机上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果计算机上已存在默认实例，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须作为命名实例安装。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 不支持在同一台计算机上并行安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的已准备实例和早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 例如，您不能并行安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例与 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的已准备实例。 但是，可以在同一台计算机上并行安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的相同主版本的多个已准备实例。 有关详细信息，请参阅 [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)。  
>   
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不能在运行 Windows Server 2008 R2 Server Core SP1 的计算机上与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本一起并行安装。 有关 Server Core 安装的详细信息，请参阅[在服务器核心上安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-on-server-core.md)。  
  
 下表显示了对 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的并行支持情况：  
  
|现有的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|并行支持|  
|--------------------------------------------------|----------------------------|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] （64 位） [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] （32 位）<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] （64 位） [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] （32 位）<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] （64 位） [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] （32 位）<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] （64 位） [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] （32 位）<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] （64 位） [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] （32 位）<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] （64 位） [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|  
  
## 防止 IP 地址冲突  
 并行安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例与 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的独立实例时，请注意避免 IP 地址上的 TCP 端口号冲突。 当 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的两个实例都配置为使用默认 TCP 端口 (1433) 时，通常会发生冲突。 要避免冲突，请将一个实例配置为使用非默认的固定端口。 在独立实例上配置固定端口通常是最简单的。 若将 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置为使用不同的端口，则在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例失败到备用节点时，将防止出现会阻止实例启动的意外 IP 地址/TCP 端口冲突  
  
## 另请参阅  
 [安装 SQL Server 2016 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [使用安装向导安装 SQL Server 2016（安装程序）](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)   
 [支持的版本升级](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [升级到 SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)   
 [SQL Server 2016 各个版本支持的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)   
 [向后兼容性_已删除](../Topic/Backward%20Compatibility_deleted.md)  
  
  