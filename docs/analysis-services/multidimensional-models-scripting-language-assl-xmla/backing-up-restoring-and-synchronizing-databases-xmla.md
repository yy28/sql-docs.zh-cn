---
title: 备份、 还原和同步数据库 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19d311a07eb11f1c5119a3c20d7536b5a2986b49
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145932"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>备份、还原和同步数据库 (XMLA)
  在 XML for Analysis 中，有三个命令分别用于备份、还原和同步数据库：  
  
-   [备份](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)命令备份[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库使用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]备份文件 (.abf)，在部分中所述[备份数据库](#backing_up_databases)。  
  
-   [还原](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)命令还原[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库从.abf 文件，如在部分中所述[还原数据库](#restoring_databases)。  
  
-   [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)命令同步一个[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库的数据和元数据的另一个数据库，在部分中所述[同步数据库](#synchronizing_databases)。  
  
##  <a name="backing_up_databases"></a> 备份数据库  
 如前文所述，**备份**命令备份指定[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库添加到备份文件。 **备份**命令有多个属性，可用于指定要备份的数据库备份的文件，若要使用，如何备份安全定义以及要备份远程分区。  
  
> [!IMPORTANT]  
>  Analysis Services 服务帐户必须对每个文件的指定备份位置拥有写入权限。 此外，用户必须具有以下角色之一：针对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的管理员角色，或对要备份的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
### <a name="specifying-the-database-and-backup-file"></a>指定数据库和备份文件  
 若要指定要备份的数据库，您设置[对象](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)的属性**备份**命令。 **对象**属性必须包含对象标识符对于数据库，否则将出错。  
  
 若要指定要创建和使用的备份过程的文件，请设置[文件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla)的属性**备份**命令。 **文件**属性应设置为要创建的备份文件的 UNC 路径和文件名称。  
  
 除了指定要用于备份的文件，还可以设置为备份文件指定以下选项：  
  
-   如果您设置[AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla)属性设为 true，**备份**命令将覆盖备份文件，如果指定的文件已存在。 如果您设置**AllowOverwrite**属性设置为 false，出现错误时，如果指定的备份文件已存在。  
  
-   如果您设置[ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla)属性设为 true，备份文件进行压缩后创建的文件。  
  
-   如果您设置[密码](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla)属性设置为任何非空值，备份文件加密通过使用指定的密码。  
  
    > [!IMPORTANT]  
    >  如果**ApplyCompression**并**密码**未指定属性时，将备份文件存储用户名和密码的包含以明文形式的连接字符串中。 以明文形式存储的数据可以被检索出来。 为了提高安全性，使用**ApplyCompression**并**密码**设置来压缩和加密备份文件。  
  
### <a name="backing-up-security-settings"></a>备份安全设置  
 [安全](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla)属性确定是否**备份**命令备份的安全定义，如角色和权限定义[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 **安全**属性还确定备份文件包含的 Windows 用户帐户和组定义为安全定义成员。  
  
 值**安全**属性仅限于下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*skipMembership*|在备份文件中包括安全定义，但不包括成员身份信息。|  
|*CopyAll*|在备份文件中包括安全定义和成员身份信息。|  
|*IgnoreSecurity*|不在备份文件中包括安全定义。|  
  
### <a name="backing-up-remote-partitions"></a>备份远程分区  
 若要备份中的远程分区[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库，设置[BackupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla)属性**备份**命令为 true。 此设置会导致**备份**命令以创建用于存储数据库的远程分区的每个远程数据源的远程备份文件。  
  
 对于要备份每个远程数据源，可以指定其相应的备份文件通过包括[位置](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla)中的元素[位置](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla)属性**备份**命令。 **位置**元素应具有其**文件**属性设置为 UNC 路径和文件名称的远程备份文件，并将其[DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceid-element-xmla)属性设置为的标识符在数据库中定义的远程数据源。  
  
##  <a name="restoring_databases"></a> 还原数据库  
 **还原**命令将还原指定[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库从备份文件。 **还原**命令有多个属性，可用于指定要备份的文件，若要使用，如何还原安全定义、 要存储的远程分区以及重新定位还原的数据库关系 OLAP (ROLAP)对象。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库中，用户必须具有以下角色之一： 服务器角色的成员[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例或具有数据库的完全控制 （管理员） 权限，要还原的数据库角色的成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
### <a name="specifying-the-database-and-backup-file"></a>指定数据库和备份文件  
 **DatabaseName**的属性**还原**命令必须包含对象标识符对于数据库，否则将出错。 如果指定的数据库已存在， **AllowOverwrite**属性确定是否覆盖现有数据库。 如果**AllowOverwrite**属性设置为 false，指定的数据库已存在，就会出错。  
  
 应设置**文件**的属性**还原**命令还原到指定的数据库的备份文件的 UNC 路径和文件名称。 您还可以设置**密码**属性指定的备份文件。 如果**密码**属性设置为任何非空值，通过使用指定的密码解密备份文件。 如果备份文件未加密，或者指定的密码与用于加密备份文件的密码不相符，则会发生错误。  
  
### <a name="restoring-security-settings"></a>还原安全设置  
 **安全**属性确定是否**还原**命令将还原的安全定义，如角色和权限定义[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 **安全**属性还确定是否**还原**命令包含的 Windows 用户帐户和组定义为安全定义成员作为还原过程的一部分。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*skipMembership*|在数据库中包括安全定义，但不包括成员身份信息。|  
|*CopyAll*|在数据库中包括安全定义和成员身份信息。|  
|*IgnoreSecurity*|不在数据库中包括安全定义。|  
  
### <a name="restoring-remote-partitions"></a>还原远程分区  
 每个远程备份文件在上一过程中创建**备份**命令时，您可以通过包括还原其关联的远程分区**位置**中的元素**位置**的属性**还原**命令。 [DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourcetype-element-xmla)属性为每个**位置**元素必须排除或显式设置为*远程*。  
  
 对于每个指定**位置**元素，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例将访问远程数据源中指定**DataSourceID**要还原的远程备份文件中定义的分区属性中指定**文件**属性。 除了**DataSourceID**并**文件**属性，以下属性可用于为每个**位置**元素用于还原远程分区：  
  
-   若要重写中指定的远程数据源的连接字符串**DataSourceID**，可以设置**ConnectionString**属性**位置**元素不同的连接字符串。 **还原**命令将使用连接字符串中包含**ConnectionString**属性。 如果**ConnectionString**未指定，则**还原**命令使用指定的远程数据源的备份文件中存储的连接字符串。 可以使用**ConnectionString**设置将远程分区移到其他远程实例。 但是，不能使用**ConnectionString**设置，以将远程分区还原到同一实例，其中包含已还原的数据库。 换而言之，不能使用**ConnectionString**属性以使到本地分区的远程分区。  
  
-   对于每个原始文件夹，用于在远程数据源上存储的远程分区，可以指定[文件夹](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla)元素以指示要还原原始文件夹中存储的所有远程分区的新文件夹。 如果**文件夹**不指定元素，则**还原**命令使用指定的远程分区的远程备份文件中包含的原始文件夹。  
  
### <a name="relocating-rolap-objects"></a>重定位 ROLAP 对象  
 **还原**命令无法还原使用 ROLAP 存储，因为此类信息存储在基础关系数据源的表中的对象的聚合或数据。 但可以还原 ROLAP 对象的元数据。 若要还原 ROLAP 对象的元数据**还原**命令重新创建关系数据源上的表结构。  
  
 可以使用**位置**中的元素**还原**重定位 ROLAP 对象的命令。 每个**位置**用来定位数据源，元素**DataSourceType**属性必须显式设置为*本地*。 您还必须设置**ConnectionString**的属性**位置**到新位置的连接字符串的元素。 在还原期间**还原**命令将通过标识的数据源的连接字符串替换为**DataSourceID**属性**位置**元素值为**ConnectionString**的属性**位置**元素。  
  
##  <a name="synchronizing_databases"></a> 同步数据库  
 **Synchronize**命令同步的数据和元数据指定的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库与另一个数据库。 **同步**命令有多个属性来指定源数据库中，如何同步安全定义、 要同步的远程分区以及 ROLAP 对象的同步。  
  
> [!NOTE]  
>  **同步**只能由服务器管理员和数据库管理员可以执行命令。 源数据库和目标数据库必须具有相同的数据库兼容级别。  
  
### <a name="specifying-the-source-database"></a>指定源数据库  
 [源](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)的属性**Synchronize**命令包含两个属性，则**ConnectionString**并**对象**。 **ConnectionString**属性包含的实例，其中包含源数据库的连接字符串和**对象**属性包含源数据库的对象标识符。  
  
 目标数据库是当前数据库的会话**同步**命令将运行。  
  
 如果**ApplyCompression**的属性**同步**命令设置为 true，从源发送的信息将数据库到目标数据库已压缩了在发送之前。  
  
### <a name="synchronizing-security-settings"></a>同步安全设置  
 [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla)属性确定是否**同步**命令同步安全定义，如角色和权限，对源数据库定义。 **SynchronizeSecurity**属性还确定是否**同步**命令包含的 Windows 用户帐户和组定义为安全定义成员。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*skipMembership*|在目标数据库中包括安全定义，但不包括成员身份信息。|  
|*CopyAll*|在目标数据库中包括安全定义和成员身份信息。|  
|*IgnoreSecurity*|不在目标数据库中包括安全定义。|  
  
### <a name="synchronizing-remote-partitions"></a>同步远程分区  
 对于源数据库中存在的每个远程数据源，可以同步每个相关联的远程分区通过包括**位置**中的元素**位置**属性**同步**命令。 每个**位置**元素， **DataSourceType**必须排除属性或显式设置为*远程*。  
  
 若要定义和连接到目标数据库中的远程数据源**Synchronize**命令使用连接字符串中定义**ConnectionString**属性**位置**元素。 **Synchronize**命令然后使用**DataSourceID**属性**位置**元素来标识要同步的远程分区。 **Synchronize**命令同步中指定的远程数据源上的远程分区**DataSourceID**对中指定的远程数据源的源数据库的属性**DataSourceID**目标数据库上的属性。  
  
 对于每个原始文件夹，用于在源数据库上的远程数据源上存储的远程分区，可以指定**文件夹**中的元素**位置**元素。 **文件夹**元素指示要在其中同步远程数据源上的原始文件夹中存储的所有远程分区的目标数据库的新文件夹。 如果**文件夹**未指定元素，Synchronize 命令将使用指定为源数据库中包含的远程分区的原始文件夹。  
  
### <a name="synchronizing-rolap-objects"></a>同步 ROLAP 对象  
 **同步**命令无法同步使用 ROLAP 存储，因为此类信息存储在基础关系数据源的表中的对象的聚合或数据。 但可以同步 ROLAP 对象的元数据。 同步元数据，**同步**命令重新创建关系数据源上的表结构。  
  
 可以使用**位置**Synchronize 命令同步 ROLAP 对象中的元素。 每个**位置**用来定位数据源，元素**DataSourceType**属性必须显式设置为*本地*。 . 您还必须设置**ConnectionString**的属性**位置**到新位置的连接字符串的元素。 在同步期间， **Synchronize**命令将通过标识的数据源的连接字符串替换为**DataSourceID**属性**位置**具有的值的元素**ConnectionString**的属性**位置**元素。  
  
## <a name="see-also"></a>另请参阅  
 [Backup 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Restore 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Synchronize 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [备份和还原 Analysis Services 数据库](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
