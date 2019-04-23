---
title: 备份、 还原和同步数据库 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- restoring databases [XML for Analysis]
- backing up databases [XML for Analysis]
- database backups [XML for Analysis]
- synchronization [XML for Analysis]
- database restores [XML for Analysis]
ms.assetid: 6c021b2e-6ad0-444e-b23f-4b5f72ce084b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6163a538c4e8872016f7ec572e4c177cfe92de94
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158803"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>备份、还原和同步数据库 (XMLA)
  在 XML for Analysis 中，有三个命令分别用于备份、还原和同步数据库：  
  
-   [备份](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)命令备份[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库使用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]备份文件 (.abf)，在部分中所述[备份数据库](#backing_up_databases)。  
  
-   [还原](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)命令还原[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库从.abf 文件，如在部分中所述[还原数据库](#restoring_databases)。  
  
-   [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)命令同步一个[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库的数据和元数据的另一个数据库，在部分中所述[同步数据库](#synchronizing_databases)。  
  
##  <a name="backing_up_databases"></a> 备份数据库  
 如前所述，`Backup` 命令将特定的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库备份到备份文件。 `Backup` 命令有多个属性，可用于指定要备份的数据库、要使用的备份文件、如何备份安全定义以及要备份的远程分区。  
  
> [!IMPORTANT]  
>  Analysis Services 服务帐户必须对每个文件的指定备份位置拥有写入权限。 此外，用户必须具有以下角色之一：针对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的管理员角色，或对要备份的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
### <a name="specifying-the-database-and-backup-file"></a>指定数据库和备份文件  
 若要指定要备份的数据库，您设置[对象](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)属性的`Backup`命令。 `Object` 属性必须包含数据库的对象标识符，否则会发生错误。  
  
 若要指定要创建和使用的备份过程的文件，请设置[文件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla)属性的`Backup`命令。 `File` 属性应设置为要创建的备份文件的 UNC 路径和文件名。  
  
 除了指定要用于备份的文件，还可以设置为备份文件指定以下选项：  
  
-   如果您设置[AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla)属性设为 true，`Backup`命令将覆盖备份文件，如果指定的文件已存在。 如果将 `AllowOverwrite` 属性设置为 false，则指定的备份文件已存在时将发生错误。  
  
-   如果您设置[ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla)属性设为 true，备份文件进行压缩后创建的文件。  
  
-   如果您设置[密码](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla)属性设置为任何非空值，备份文件加密通过使用指定的密码。  
  
    > [!IMPORTANT]  
    >  如果未指定 `ApplyCompression` 和 `Password` 属性，备份文件将以明文形式存储连接字符串中包含的用户名和密码。 以明文形式存储的数据可以被检索出来。 为了提高安全性，请使用 `ApplyCompression` 和 `Password` 设置来压缩和加密备份文件。  
  
### <a name="backing-up-security-settings"></a>备份安全设置  
 [安全](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla)属性确定是否`Backup`命令备份的安全定义，如角色和权限定义[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 `Security` 属性还确定备份文件是否包含定义为安全定义成员的 Windows 用户帐户和用户组。  
  
 `Security` 属性的值限制为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*SkipMembership*|在备份文件中包括安全定义，但不包括成员身份信息。|  
|*CopyAll*|在备份文件中包括安全定义和成员身份信息。|  
|*IgnoreSecurity*|不在备份文件中包括安全定义。|  
  
### <a name="backing-up-remote-partitions"></a>备份远程分区  
 若要备份中的远程分区[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库，设置[BackupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla)属性`Backup`命令为 true。 此设置将使 `Backup` 命令为用于存储数据库的远程分区的每个远程数据源创建一个远程备份文件。  
  
 对于要备份每个远程数据源，可以指定其相应的备份文件通过包括[位置](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla)中的元素[位置](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla)属性`Backup`命令。 `Location`元素应具有其`File`属性设置为 UNC 路径和文件名称的远程备份文件，并将其[DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)在数据库中定义的属性设置为远程数据源的标识符。  
  
##  <a name="restoring_databases"></a> 还原数据库  
 `Restore` 命令从备份文件中还原指定的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。 `Restore` 命令有多个属性，可用于指定要还原的数据库、要使用的备份文件、如何还原安全定义、要存储的远程分区以及关系 OLAP (ROLAP) 对象的重定位。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库中，用户必须具有以下角色之一： 服务器角色的成员[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例或具有数据库的完全控制 （管理员） 权限，要还原的数据库角色的成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
### <a name="specifying-the-database-and-backup-file"></a>指定数据库和备份文件  
 `DatabaseName` 命令的 `Restore` 属性必须包含数据库的对象标识符，否则会发生错误。 如果指定的数据库已经存在，`AllowOverwrite` 属性将确定是否覆盖现有数据库。 如果 `AllowOverwrite` 属性设置为 false 并且指定的数据库已经存在，则将发生错误。  
  
 应将 `File` 命令的 `Restore` 属性设置为要还原到指定数据库的备份文件的 UNC 路径和文件名。 还可以设置指定备份文件的 `Password` 属性。 如果 `Password` 属性设置为任何非空值，则将使用该指定密码对备份文件进行解密。 如果备份文件未加密，或者指定的密码与用于加密备份文件的密码不相符，则会发生错误。  
  
### <a name="restoring-security-settings"></a>还原安全设置  
 `Security` 属性确定 `Restore` 命令是否还原对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库定义的安全定义，如角色和权限。 `Security` 属性还确定 `Restore` 命令是否包含定义为安全定义成员的 Windows 用户帐户和用户组作为还原过程的一部分。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*SkipMembership*|在数据库中包括安全定义，但不包括成员身份信息。|  
|*CopyAll*|在数据库中包括安全定义和成员身份信息。|  
|*IgnoreSecurity*|不在数据库中包括安全定义。|  
  
### <a name="restoring-remote-partitions"></a>还原远程分区  
 对于在前述 `Backup` 命令中创建的每个远程备份文件，可以通过在 `Location` 命令的 `Locations` 属性中包含一个 `Restore` 元素来还原该备份文件的相关远程分区。 [DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)属性为每个`Location`必须显式设置为或者不包含元素*远程*。  
  
 对于每个指定的 `Location` 元素，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例将访问在 `DataSourceID` 属性中指定的远程数据源，以还原在 `File` 属性中指定的远程备份文件中定义的分区。 除了 `DataSourceID` 和 `File` 属性外，下列属性也可供每个 `Location` 元素用于还原远程分区：  
  
-   若要覆盖在 `DataSourceID` 中指定的远程数据源的连接字符串，可将 `ConnectionString` 元素的 `Location` 属性设置为其他连接字符串。 此时，`Restore` 命令将使用 `ConnectionString` 属性中包含的连接字符串。 如果未指定 `ConnectionString`，`Restore` 命令将使用指定的远程数据源的备份文件中存储的连接字符串。 可以使用 `ConnectionString` 设置将远程分区移到其他远程实例。 但是不能使用 `ConnectionString` 设置将远程分区还原到包含已还原的数据库的同一实例。 换言之，不能使用 `ConnectionString` 属性将远程分区放入本地分区。  
  
-   对于每个原始文件夹，用于在远程数据源上存储的远程分区，可以指定[文件夹](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla)元素以指示要还原原始文件夹中存储的所有远程分区的新文件夹。 如果未指定 `Folder` 元素，`Restore` 命令将使用远程备份文件中包含的为远程分区指定的原始文件夹。  
  
### <a name="relocating-rolap-objects"></a>重定位 ROLAP 对象  
 `Restore` 命令无法还原使用 ROLAP 存储的对象的聚合或数据，因为此类信息存储在基础关系数据源的表中。 但可以还原 ROLAP 对象的元数据。 为了还原 ROLAP 对象的元数据，`Restore` 命令会对关系数据源重新创建表结构。  
  
 可以使用 `Location` 命令中的 `Restore` 元素重定位 ROLAP 对象。 每个`Location`元素用于重新定位数据源`DataSourceType`属性必须显式设置为*本地*。 还必须将 `ConnectionString` 元素的 `Location` 属性设置为新位置的连接字符串。 在还原过程中，`Restore` 命令将使用 `DataSourceID` 元素的 `Location` 属性的值替换由 `ConnectionString` 元素的 `Location` 属性标识的数据源的连接字符串。  
  
##  <a name="synchronizing_databases"></a> 同步数据库  
 `Synchronize` 命令同步指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库和另一数据库的数据和元数据。 `Synchronize` 命令有多个属性，可用于指定源数据库、如何同步安全定义、要同步的远程分区以及 ROLAP 对象的同步。  
  
> [!NOTE]  
>  只有服务器管理员和数据库管理员可以执行 `Synchronize` 命令。 源数据库和目标数据库必须具有相同的数据库兼容级别。  
  
### <a name="specifying-the-source-database"></a>指定源数据库  
 [源](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)的属性`Synchronize`命令包含两个属性，则`ConnectionString`和`Object`。 `ConnectionString` 属性包含源数据库所属实例的连接字符串，`Object` 属性包含源数据库的对象标识符。  
  
 目标数据库是 `Synchronize` 命令在其中运行的会话的当前数据库。  
  
 如果 `ApplyCompression` 命令的 `Synchronize` 属性设置为 true，从源数据库发送到目标数据库的信息将在发送前进行压缩。  
  
### <a name="synchronizing-security-settings"></a>同步安全设置  
 [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla)属性确定是否`Synchronize`命令同步安全定义，如角色和权限，对源数据库定义。 `SynchronizeSecurity` 属性还确定 `Sychronize` 命令是否包含定义为安全定义成员的 Windows 用户帐户和用户组。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*SkipMembership*|在目标数据库中包括安全定义，但不包括成员身份信息。|  
|*CopyAll*|在目标数据库中包括安全定义和成员身份信息。|  
|*IgnoreSecurity*|不在目标数据库中包括安全定义。|  
  
### <a name="synchronizing-remote-partitions"></a>同步远程分区  
 对于源数据库中存在的每个远程数据源，可以通过在 `Location` 命令的 `Locations` 属性中包含一个 `Synchronize` 元素来同步每个关联的远程分区。 每个`Location`元素中，`DataSourceType`属性必须排除或显式设置为*远程*。  
  
 为了定义和连接到目标数据库中的远程数据源，`Synchronize` 命令使用在 `ConnectionString` 元素的 `Location` 属性中定义的连接字符串。 然后，`Synchronize` 命令使用 `DataSourceID` 元素的 `Location` 属性标识要同步的远程分区。 `Synchronize`命令同步中指定的远程数据源上的远程分区`DataSourceID`属性中指定的远程数据源的源数据库上`DataSourceID`目标数据库上的属性。  
  
 对于用于在源数据库的远程数据源中存储远程分区的每个原始文件夹，还可以在 `Folder` 元素中指定 `Location` 元素。 `Folder` 元素指示目标数据库的新文件夹，要将该文件夹中的分区与远程数据源中原始文件夹中存储的所有远程分区同步。 如果未指定 `Folder` 元素，Synchronize 命令将使用源数据库中包含的为远程分区指定的原始文件夹。  
  
### <a name="synchronizing-rolap-objects"></a>同步 ROLAP 对象  
 `Synchronize` 命令无法同步使用 ROLAP 存储的对象的聚合或数据，因为此类信息存储在基础关系数据源的表中。 但可以同步 ROLAP 对象的元数据。 为了同步元数据，`Synchronize` 命令会对关系数据源重新创建表结构。  
  
 可以使用 Synchronize 命令中的 `Location` 元素同步 ROLAP 对象。 每个`Location`元素用于重新定位数据源`DataSourceType`属性必须显式设置为*本地*。 . 还必须将 `ConnectionString` 元素的 `Location` 属性设置为新位置的连接字符串。 在同步过程中，`Synchronize` 命令将使用 `DataSourceID` 元素的 `Location` 属性的值替换由 `ConnectionString` 元素的 `Location` 属性标识的数据源的连接字符串。  
  
## <a name="see-also"></a>请参阅  
 [Backup 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Restore 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Synchronize 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [备份和还原 Analysis Services 数据库](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
