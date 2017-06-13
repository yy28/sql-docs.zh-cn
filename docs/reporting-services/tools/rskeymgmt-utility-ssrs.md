---
title: "rskeymgmt 实用工具 (SSRS) |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], encryption
- joining report server instances [SQL Server]
- report server scale-out deployments [Reporting Services]
- cryptography [Reporting Services]
- multiple report server instances
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], scale-out deployments
- encryption [Reporting Services]
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 53f1318d-bd2d-4c08-b19f-c8b698b5b3d3
caps.latest.revision: 56
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 95e64239c30aab1a341c281230c887f9668b9277
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="rskeymgmt-utility-ssrs"></a>rskeymgmt 实用工具 (SSRS)
  提取、还原、创建以及删除对称密钥，该密钥用于保护敏感报表服务器数据免受未经授权的访问。 此实用工具还用于将报表服务器实例加入扩展部署。 报表服务器扩展部署是指共享单个报表服务器数据库的多个报表服务器实例。  
  
## <a name="syntax"></a>语法  
  
```  
  
rskeymgmt {-?}  
{–eextract}  
{–aapply}  
{-ddeleteall}  
{–srecreatekey}  
{–rremoveinstancekey}  
{-jjoinfarm}  
{-iinstance}  
{-ffile}  
{-pencryptionpassword}  
{-mremotecomputer}  
{-ninstancenameofremotecomputer}  
{-uadministratoruseraccount}  
{-vadministratorpassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>参数  
 **-?**  
 显示 **rskeymgmt** 参数的语法。  
  
 **-e**  
 提取为报表服务器数据加密和解密所用的对称密钥，以便将其复制到文件中。  
  
 此参数不带值。 但是，您必须在命令行中包含其他参数，才能完成提取。 必须指定的参数包括 **-f** 和**-p**。  
  
 **-a**  
 使用受密码保护的备份文件中提供的副本替换现有对称密钥。 这将会更新对称密钥的所有实例。  
  
 此参数不带值。 但是，您必须在命令行中包含其他参数，才能选择包含要应用的密钥的文件。 可以指定的参数包括 **-f** 和**-p**。  
  
 **-d**  
 删除报表服务器数据库中的所有对称密钥实例和所有加密数据。 此参数不带值。  
  
 **-s**  
 生成新的对称密钥，并使用新密钥重新加密所有已加密的内容。 重新生成对称密钥的所有实例。  
  
 **-j**  
 配置远程报表服务器实例，以共享本地报表服务器实例所用的报表服务器数据库。  
  
 **-r**  *installationID*  
 删除特定报表服务器实例的对称密钥信息，从而从扩展部署中删除报表服务器。 *installationID* 是 RSReportserver.config 文件中的 GUID 值。  
  
 **-f**  *file*  
 指定一个指向存储对称密钥备份副本的文件的完全限定路径。  
  
 对于 **rskeymgmt -e**，对称密钥将写入你指定的文件中。  
  
 对于 **rskeymgmt -a**，存储在该文件中的对称密钥值将应用于报表服务器实例。  
  
 **-p**  *password*  
 （ **-f**为必需）指定用于备份或应用对称密钥的密码。 该值不能为空。  
  
 **-i**  
 指定本地报表服务器实例。 如果已在默认的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中安装了报表服务器，则此参数是可选的（ **-i** 的默认值为 MSSQLSERVER）。 如果已按命名实例的形式安装了报表服务器，则 **-i** 为必需项。  
  
 **-m**  
 指定远程计算机名称，该计算机将承载加入报表服务器扩展部署的报表服务器实例。 请使用网络中标识该计算机的计算机名称。  
  
 **-n**  
 指定远程计算机上报表服务器实例的名称。 此参数是可选的如果将报表服务器安装在默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例 (默认值为 **-n** 为 MSSQLSERVER)。 如果将报表服务器安装为命名实例，  **-n** 是必需的。  
  
 **-u**  *useraccount*  
 指定要加入扩展部署的远程计算机上的管理员帐户。 如果未指定帐户，则使用当前用户的凭据。  
  
 **-v**  *password*  
 （ **-u**为必需）指定要加入扩展部署的远程计算机上管理员帐户的密码。  
  
 **-t**  *trace*  
 将错误消息输出到跟踪日志。 此参数不带值。 有关详细信息，请参阅 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)。  
  
## <a name="permissions"></a>Permissions  
 只有本地管理员才能运行此工具，并且必须在承载报表服务器的计算机本地运行。 rskeymgmt 实用工具用于本地报表服务器 Windows 实例。该实用工具不能连接到远程报表服务器 Windows 服务实例，因此无法用于管理远程报表服务器实例的加密密钥。  
  
> [!NOTE]  
>  如果使用 **-u** 和 **-v** 参数，请指定在远程计算机中具有管理员权限的帐户。  
  
## <a name="examples"></a>示例  
 以下示例阐释了 **rskeymgmt**的使用方法。 这些示例将说明如何提取、还原以及删除加密密钥，并显示如何配置报表服务器扩展部署。  
  
#### <a name="extracting-encryption-keys"></a>提取加密密钥  
 此示例显示如何创建加密密钥备份副本，并将其保存到软盘中密码保护的文件中。 如果报表服务器是作为命名实例安装的，则添加 **-i** 参数。  
  
```  
rskeymgmt -e -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="restoring-encryption-keys"></a>还原加密密钥  
 此示例显示如何替换加密密钥。 您必须指定密钥备份副本的位置以及该文件的解锁密码。  
  
```  
rskeymgmt -a -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="deleting-encryption-keys-and-encrypted-content"></a>删除加密密钥和加密的内容  
 此示例显示如何删除报表服务器中存储的所有加密密钥。 如果安装的是报表服务器扩展部署，则将删除部署中包括的所有报表服务器实例的加密密钥。 删除加密密钥还会删除报表服务器数据库中现有的全部已加密值。 有关加密内容的详细信息，请参阅[存储加密的 Report Server 数据 (SSRS Configuration Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)。  
  
```  
rskeymgmt -d  
```  
  
#### <a name="joining-a-remote-report-server-named-instance-to-a-scale-out-deployment"></a>将远程报表服务器命名实例加入扩展部署  
 此示例显示如何将远程计算机上安装的报表服务器实例添加到报表服务器扩展部署中。 您必须在已配置为使用共享数据库的某台计算机上运行该命令。 命令参数指定了要加入到扩展部署的远程报表服务器实例。  
  
```  
rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
```  
  
> [!NOTE]  
>  报表服务器扩展部署是指多个报表服务器实例共享同一报表服务器数据库的部署模型。 任何报表服务器实例，只要将其对称密钥存储在一个报表服务器数据库中，就可以使用该数据库。 例如，如果报表服务器数据库包含三个报表服务器实例的密钥信息，则所有这三个实例均被视为同一扩展部署的成员。  
  
#### <a name="joining-report-server-instances-on-the-same-computer"></a>联接同一台计算机上的报表服务器实例  
 可以从安装在同一台计算机上的多个报表服务器实例创建扩展部署。 如果要联接本地安装的报表服务器实例，请不要设置 **-u** 和 **-v** 参数。 仅当联接远程计算机中的实例时才需使用 **-u** 和 **-v** 参数。 如果指定这些参数，您将收到以下错误：“用户凭据不能用于本地连接”。  
  
 以下示例说明了使用多个本地实例创建扩展部署的语法。 在此示例中， \< **initializedinstance**> 是已初始化为使用报表服务器数据库中，实例的名称和\< **newinstance**> 是你想要添加到部署的实例名称：  
  
```  
rskeymgmt -j -i <initializedinstance> -m <computer name> -n <newinstance>  
```  
  
#### <a name="removing-encryption-keys-for-a-single-report-server-in-a-scale-out-deployment"></a>删除扩展部署中单个报表服务器的加密密钥  
 此示例显示如何删除报表服务器扩展部署中单个报表服务器的加密密钥。 将从报表服务器数据库中删除密钥。 一旦报表服务器实例的密钥被删除，该报表服务器实例便不再能访问该数据库中的加密数据，这就意味着已将其从扩展部署中有效删除。  
  
 从扩展部署中删除报表服务器实例要求您指定安装 ID。 安装 ID 是 GUID，它存储在要删除其加密密钥的报表服务器实例的 RSReportserver.config 文件中。 您必须在要从扩展部署中删除的计算机上运行以下命令。 如果报表服务器作为命名实例安装，则可使用 **-i** 参数指定实例。 有关详细信息，请参阅 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。  
  
```  
rskeymgmt -r <installationID>  
```  
  
## <a name="file-location"></a>文件位置  
 Rskeymgmt.exe 位于 ** \<*驱动器*>: files\microsoft SQL Server\110\Tools\Binn * * 或在* * \<*驱动器*>: \Program 文件 (x86) \Microsoft SQL Server\110\Tools\Binn**。 可以在文件系统的任何文件夹中运行此实用工具。  
  
## <a name="remarks"></a>注释  
 报表服务器对存储的凭据和连接信息进行加密。 公钥和对称密钥可用于对数据进行加密。 要运行报表服务器，报表服务器数据库必须具有有效的密钥。 你可以使用 **rskeymgmt** 来备份、删除或还原密钥。 如果无法还原密钥，此工具将为您提供一种方法，以删除不再使用的加密内容。  
  
 **rskeymgmt** 实用工具用于管理在安装或初始化期间定义的密钥集。 它通过远程过程调用 (RPC) 端点连接到本地报表服务器 Windows 服务。 必须运行报表服务器 Windows 服务才能使用此实用工具。  
  
 有关加密密钥的详细信息，请参阅[配置和管理加密密钥 (SSRS Configuration Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md) 和[初始化报表服务器 (SSRS Configuration Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [扩展部署 - Reporting Services 本机模式 (Configuration Manager)](http://msdn.microsoft.com/library/4df38294-6f9d-4b40-9f03-1f01c1f0700c)   
 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [报表服务器命令提示实用工具 (SSRS)](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
 [配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
