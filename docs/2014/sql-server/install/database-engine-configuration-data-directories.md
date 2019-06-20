---
title: 数据库引擎配置-数据目录 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9b1fa0fc-623b-479a-afc3-4f13bd850487
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfb62ec0bbd16a2b77e2f05f64d36ef31498a100
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095903"
---
# <a name="database-engine-configuration---data-directories"></a>数据库引擎配置 - 数据目录
  使用此页面可指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 程序和数据文件的安装位置。 根据安装类型，支持的存储可能包括本地磁盘、共享存储或 SMB 文件服务器。  
  
 若要将 SMB 文件共享指定为目录，您必须手动键入支持的 UNC 路径。 不支持浏览到 SMB 文件共享。 下面是 SMB 文件共享支持的 UNC 路径格式： \\\Servername\ShareName\\....  
  
## <a name="stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的独立实例  
 下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的独立实例支持的存储类型和默认目录，用户可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中配置这些内容。  
  
## <a name="uielement-list"></a>UIElement 列表  
  
|Description|支持的存储类型|默认目录|建议|  
|-----------------|----------------------------|-----------------------|---------------------|  
|数据根目录|本地磁盘、 SMB 文件服务器、 共享存储<sup>1</sup>|C:\Program Files\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \| [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序将配置的 Acl[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目录和配置过程中的中断继承。|  
|用户数据库目录|本地磁盘、 SMB 文件服务器、 共享存储<sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。\<InstanceID > \MSSQL\Data|用户数据目录的最佳实践取决于工作量和性能要求。|  
|用户数据库日志目录|本地磁盘、 SMB 文件服务器、 共享存储<sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。\<InstanceID > \MSSQL\Data|确保日志目录有足够的空间。|  
|临时数据库目录|本地磁盘、 SMB 文件服务器、 共享存储<sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。\<InstanceID > \MSSQL\Data|Temp 目录的最佳实践取决于工作量和性能要求。|  
|临时数据库日志目录|本地磁盘、 SMB 文件服务器、 共享存储<sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。\<InstanceID > \MSSQL\Data|确保日志目录有足够的空间。|  
|备份目录|本地磁盘、 SMB 文件服务器、 共享存储<sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。\<InstanceID > \MSSQL\Backup|设置合适的权限以防止数据丢失，并确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的用户帐户具有写入备份目录的足够权限。 不支持对备份目录使用映射的驱动器。|  
  
 <sup>1</sup>尽管支持共享的磁盘，但它不是独立实例的做法，建议的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例  
 下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的故障转移群集实例支持的存储类型和默认目录，用户可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中配置这些内容。  
  
|Description|支持的存储类型|默认目录|建议|  
|-----------------|----------------------------|-----------------------|---------------------|  
|数据根目录|共享存储、SMB 文件服务器|\<驱动器:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> 提示：如果在“群集磁盘选择”页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录配置 ACL 并在配置过程中中断继承。|  
|用户数据库目录|共享存储、SMB 文件服务器|\<驱动器： > 程序文件\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。\<InstanceID > \MSSQL\Data<br /><br /> 提示：如果在“群集磁盘选择”页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|用户数据目录的最佳实践取决于工作量和性能要求。|  
|用户数据库日志目录|共享存储、SMB 文件服务器|\<驱动器： > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。\<InstanceID > \MSSQL\Data<br /><br /> 提示：如果在“群集磁盘选择”页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|确保日志目录有足够的空间。|  
|临时数据库目录|本地磁盘、共享存储、SMB 文件服务器|\<驱动器： > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。\<InstanceID > \MSSQL\Data<br /><br /> 提示：如果在“群集磁盘选择”页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|请确保指定的目录对所有群集节点都有效。 在故障转移期间，如果 tempdb 目录对故障转移目标节点不可用，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源将无法联机。|  
|临时数据库日志目录|本地磁盘、共享存储、SMB 文件服务器|\<驱动器： > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。\<InstanceID > \MSSQL\Data<br /><br /> 提示：如果在“群集磁盘选择”页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|请确保指定的目录对所有群集节点都有效。 在故障转移期间，如果 tempdb 目录对故障转移目标节点不可用，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源将无法联机。|  
|备份目录|本地磁盘、共享存储、SMB 文件服务器|\<驱动器： > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。\<InstanceID > \MSSQL\Backup<br /><br /> 提示：如果在“群集磁盘选择”页上选择了共享磁盘，则默认设置为第一个共享磁盘。 如果在 **“群集磁盘选择”** 页上没有进行任何选择，此字段默认为空。|设置合适的权限以防止数据丢失，并确保 SQL Server 服务的用户帐户具有写入备份目录的足够权限。 不支持对备份目录使用映射的驱动器。|  
  
## <a name="security-considerations"></a>需要考虑的安全性因素  
 安装程序将为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录配置 ACL 并在配置过程中中断继承。  
  
 以下建议适用于 SMB 文件服务器：  
  
-   使用 SMB 文件服务器时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户必须是域帐户。  
  
-   用于安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帐户应对用作数据目录的 SMB 文件共享文件夹具有 FULL CONTROL NTFS 权限。  
  
-   用于安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帐户应具有对 SMB 文件服务器的 SeSecurityPrivilege 特权。 若要授予此特权，请使用文件服务器上的“本地安全策略”控制台将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装帐户添加到 **“管理审核和安全日志”** 策略中。 在 **“本地安全策略”** 控制台中 **“本地策略”** 下的 **“用户权限分配”** 部分可以找到此设置。  
  
## <a name="notes"></a>说明  
  
-   向现有安装中添加功能时，不能更改先前安装的功能的位置，也不能为新功能指定该位置。  
  
-   如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件也应安装到单独的目录。  
  
-   在下列情况下，不能安装程序文件和数据文件：  
  
    -   在可移动磁盘驱动器上  
  
    -   在使用压缩的文件系统上  
  
    -   在系统文件所在的目录上  
  
    -   在故障转移群集实例的映射网络驱动器上  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 的默认实例和命名实例的文件位置](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [文件服务器上的共享权限和 NTFS 权限](https://go.microsoft.com/fwlink/?LinkID=206571)  
  
  
