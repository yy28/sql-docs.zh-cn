---
title: 备份、 还原和同步数据库 (XMLA) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3bb12c60f38049a9a860a3ce5f425559ca7a51e8
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>备份、还原和同步数据库 (XMLA)
  在 XML for Analysis 中，有三个命令分别用于备份、还原和同步数据库：  
  
-   [备份](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)命令备份[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库使用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]备份文件 (.abf)，部分中所述[备份数据库](#backing_up_databases)。  
  
-   [还原](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)命令还原[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部分中所述从.abf 文件，数据库[Restoring Databases](#restoring_databases)。  
  
-   [同步](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)命令将一个同步[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部分中所述，使用数据和元数据的另一个数据库数据库[同步数据库](#synchronizing_databases)。  
  
##  <a name="backing_up_databases"></a> 备份数据库  
 如前所述，**备份**命令备份指定[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]到备份文件的数据库。 **备份**命令具有各种属性，可让你指定要备份的数据库备份的文件，若要使用，如何备份安全定义和要备份远程分区。  
  
> [!IMPORTANT]  
>  Analysis Services 服务帐户必须对每个文件的指定备份位置拥有写入权限。 此外，用户必须具有以下角色之一：针对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的管理员角色，或对要备份的数据库拥有完全控制（管理员）权限的数据库角色成员。  
  
### <a name="specifying-the-database-and-backup-file"></a>指定数据库和备份文件  
 若要指定要备份的数据库，你可以设置[对象](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)属性**备份**命令。 **对象**属性必须包含对象标识符对于数据库，否则将发生错误。  
  
 若要指定文件的创建和使用由备份过程，你可以设置[文件](../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)属性**备份**命令。 **文件**属性应设置为要创建的备份文件的 UNC 路径和文件名称。  
  
 除了指定要用于备份的文件，还可以设置为备份文件指定以下选项：  
  
-   如果你设置[AllowOverwrite](../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)属性为 true，**备份**命令将覆盖备份文件，如果指定的文件已存在。 如果你设置**AllowOverwrite**属性设置为 false，出现错误时，如果指定的备份文件已存在。  
  
-   如果你设置[ApplyCompression](../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md)属性为 true，备份文件进行压缩后的文件创建的。  
  
-   如果你设置[密码](../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md)通过使用指定的密码加密为任何非空值，备份文件的属性。  
  
    > [!IMPORTANT]  
    >  如果**ApplyCompression**和**密码**不指定属性、 备份文件将存储用户名和密码包含在连接字符串以明文形式。 以明文形式存储的数据可以被检索出来。 为了提高安全性，使用**ApplyCompression**和**密码**设置应用于同时压缩和加密备份文件。  
  
### <a name="backing-up-security-settings"></a>备份安全设置  
 [安全](../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)属性确定是否**备份**命令备份安全定义，如上定义角色和权限，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 **安全**属性还确定备份文件包含的 Windows 用户帐户和组定义为安全定义的成员。  
  
 值**安全**属性仅限于下表中列出的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*skipMembership*|在备份文件中包括安全定义，但不包括成员身份信息。|  
|*CopyAll*|在备份文件中包括安全定义和成员身份信息。|  
|*IgnoreSecurity*|不在备份文件中包括安全定义。|  
  
### <a name="backing-up-remote-partitions"></a>备份远程分区  
 若要备份中的远程分区[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库，你将设置[BackupRemotePartitions](../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)属性**备份**命令为 true。 此设置会导致**备份**命令以创建用于存储数据库的远程分区的每个远程数据源的远程备份文件。  
  
 对于要备份每个远程数据源中,，你可以指定其相应的备份文件通过包括[位置](../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)中的元素[位置](../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)属性**备份**命令。 **位置**元素应具有其**文件**属性设置为远程的备份文件的 UNC 路径和文件名称并将其[DataSourceID](../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)属性设置为的标识符在数据库中定义的远程数据源。  
  
##  <a name="restoring_databases"></a> 还原数据库  
 **还原**命令会将还原指定[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]从备份文件的数据库。 **还原**命令具有各种属性，可让你指定要还原的备份文件，若要使用，如何还原安全定义、 远程分区要存储和重新分配的数据库关系 OLAP (ROLAP)对象。  
  
> [!IMPORTANT]  
>  对于每个备份文件，运行还原命令的用户必须对每个文件的指定备份位置具有读取权限。 若要还原未在服务器上安装的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，用户还必须是此 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器角色成员。 若要覆盖[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库，用户必须具有以下角色之一： 服务器角色的成员[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例或具有要还原数据库的 （管理员） 的完全控制权限的数据库角色的成员。  
  
> [!NOTE]  
>  还原现有数据库之后，还原了此数据库的用户可能会失去对还原后的数据库的访问权限。 如果在执行备份时用户不是服务器角色成员或者不是拥有完全控制（管理员）权限的数据库角色成员，则会出现这种失去访问权限的情形。  
  
### <a name="specifying-the-database-and-backup-file"></a>指定数据库和备份文件  
 **DatabaseName**属性**还原**命令必须包含对象标识符对于数据库，否则将发生错误。 如果指定的数据库已存在， **AllowOverwrite**属性确定是否覆盖现有数据库。 如果**AllowOverwrite**属性设置为 false，指定的数据库已存在，则会出错。  
  
 应设置**文件**属性**还原**命令到要还原到指定的数据库的备份文件的 UNC 路径和文件名称。 你还可以设置**密码**指定备份文件的属性。 如果**密码**属性设置为任何非空值，通过使用指定的密码解密备份的文件。 如果备份文件未加密，或者指定的密码与用于加密备份文件的密码不相符，则会发生错误。  
  
### <a name="restoring-security-settings"></a>还原安全设置  
 **安全**属性确定是否**还原**命令还原安全定义，如角色和权限，在上定义[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 **安全**属性也确定是否**还原**命令包含的 Windows 用户帐户和组为安全定义的成员定义为在还原过程的一部分。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*skipMembership*|在数据库中包括安全定义，但不包括成员身份信息。|  
|*CopyAll*|在数据库中包括安全定义和成员身份信息。|  
|*IgnoreSecurity*|不在数据库中包括安全定义。|  
  
### <a name="restoring-remote-partitions"></a>还原远程分区  
 在上一个过程中创建每个远程备份文件的**备份**命令时，你可以通过包括还原其关联的远程分区**位置**中的元素**位置**属性**还原**命令。 [DataSourceType](../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md)每个属性**位置**必须排除元素，或将其显式设置为*远程*。  
  
 为每个指定**位置**元素，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例联系中指定的远程数据源**DataSourceID**还原远程备份文件中定义的分区的属性指定在**文件**属性。 除了**DataSourceID**和**文件**属性，以下属性可用于每个**位置**元素，用于还原远程分区：  
  
-   若要重写中指定的远程数据源的连接字符串**DataSourceID**，你可以设置**ConnectionString**属性**位置**元素不同的连接字符串。 **还原**命令然后将使用连接字符串中包含**ConnectionString**属性。 如果**ConnectionString**未指定，**还原**命令使用指定的远程数据源的备份文件中存储的连接字符串。 你可以使用**ConnectionString**设置以将远程分区移动到不同的远程实例。 但是，不能使用**ConnectionString**设置还原到同一个实例，其中包含已还原的数据库的远程分区。 换而言之，你不能使用**ConnectionString**属性以使到本地分区的远程分区。  
  
-   对于每个原始文件夹用于存储在远程数据源上的远程分区，你可以指定[文件夹](../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)元素以指示在其中以还原存储在原始文件夹中的所有远程分区的新文件夹。 如果**文件夹**元素未指定，**还原**命令使用指定的远程分区的远程备份文件中包含的原始文件夹。  
  
### <a name="relocating-rolap-objects"></a>重定位 ROLAP 对象  
 **还原**命令无法还原聚合或使用 ROLAP 存储，因为此类信息存储在基础关系数据源上的表中的对象的数据。 但可以还原 ROLAP 对象的元数据。 若要还原 ROLAP 对象的元数据**还原**命令重新创建关系数据源上的表结构。  
  
 你可以使用**位置**中的元素**还原**命令来重新定位 ROLAP 对象。 每个**位置**元素，用于重新定位数据源， **DataSourceType**属性必须显式设置为*本地*。 你还必须设置**ConnectionString**属性**位置**到新位置的连接字符串的元素。 在还原期间，**还原**命令将替换由标识数据源的连接字符串**DataSourceID**属性**位置**元素值为**ConnectionString**属性**位置**元素。  
  
##  <a name="synchronizing_databases"></a> 同步数据库  
 **同步**命令同步的数据和元数据指定的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]与另一个数据库的数据库。 **同步**命令具有允许你指定的源数据库的各种属性如何同步安全定义、 远程分区同步和 ROLAP 对象的同步。  
  
> [!NOTE]  
>  **同步**只能由服务器管理员和数据库管理员可以执行命令。 源数据库和目标数据库必须具有相同的数据库兼容级别。  
  
### <a name="specifying-the-source-database"></a>指定源数据库  
 [源](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)属性**同步**命令包含两个属性， **ConnectionString**和**对象**。 **ConnectionString**属性包含的实例，其中包含源数据库的连接字符串和**对象**属性包含源数据库的对象标识符。  
  
 目标数据库的会话是当前数据库**同步**命令将运行。  
  
 如果**ApplyCompression**属性**同步**命令设置为 true，从源系统发送的信息数据库部署到目标数据库压缩在发送之前。  
  
### <a name="synchronizing-security-settings"></a>同步安全设置  
 [SynchronizeSecurity](../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md)属性确定是否**同步**命令同步的安全定义，如角色和权限，对源数据库已定义。 **SynchronizeSecurity**属性也确定是否**小心地同步**命令包含的 Windows 用户帐户和组定义为安全定义的成员。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*skipMembership*|在目标数据库中包括安全定义，但不包括成员身份信息。|  
|*CopyAll*|在目标数据库中包括安全定义和成员身份信息。|  
|*IgnoreSecurity*|不在目标数据库中包括安全定义。|  
  
### <a name="synchronizing-remote-partitions"></a>同步远程分区  
 对于每个存在于源数据库的远程数据源，您可以每个关联的远程分区通过同步包括**位置**中的元素**位置**属性**同步**命令。 每个**位置**元素， **DataSourceType**必须排除属性或将其显式设置为*远程*。  
  
 定义并将连接到目标数据库中的远程数据源**同步**命令使用连接字符串中定义**ConnectionString**属性**位置**元素。 **同步**命令然后使用**DataSourceID**属性**位置**元素可以标识要同步哪些远程分区。 **同步**命令同步中指定的远程数据源上的远程分区**DataSourceID**对中指定的远程数据源的源数据库的属性**DataSourceID**目标数据库上的属性。  
  
 对于每个原始文件夹用于在源数据库上的远程数据源上存储的远程分区，你还可以指定**文件夹**中的元素**位置**元素。 **文件夹**元素指示要在其中同步远程数据源上的原始文件夹中存储的所有远程分区的目标数据库的新文件夹。 如果**文件夹**元素未指定，则同步命令使用指定为源数据库中包含的远程分区的原始文件夹。  
  
### <a name="synchronizing-rolap-objects"></a>同步 ROLAP 对象  
 **同步**命令无法同步聚合或使用 ROLAP 存储，因为此类信息存储在基础关系数据源上的表中的对象的数据。 但可以同步 ROLAP 对象的元数据。 同步元数据，**同步**命令重新创建关系数据源上的表结构。  
  
 你可以使用**位置**Synchronize 命令同步 ROLAP 对象中的元素。 每个**位置**元素，用于重新定位数据源， **DataSourceType**属性必须显式设置为*本地*。 。 你还必须设置**ConnectionString**属性**位置**到新位置的连接字符串的元素。 在同步期间，**同步**命令将替换由标识数据源的连接字符串**DataSourceID**属性**位置**具有值的元素**ConnectionString**属性**位置**元素。  
  
## <a name="see-also"></a>另请参阅  
 [Backup 元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [还原元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [同步元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [备份和还原 Analysis Services 数据库](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
