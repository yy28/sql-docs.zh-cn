---
title: 删除和重新创建加密密钥（SSRS 配置管理器）| Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- re-creating encryption keys
- encryption keys [Reporting Services]
- deleting encryption keys
- symmetric keys [Reporting Services]
- removing encryption keys
- resetting encryption keys
ms.assetid: 201afe5f-acc9-4a37-b5ec-121dc7df2a61
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5bf83ea3eb7ed7f4ef28872b964449d2924aab48
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593536"
---
# <a name="ssrs-encryption-keys---delete-and-re-create-encryption-keys"></a>SSRS 加密密钥 - 删除和重新创建加密密钥
  删除和重新创建加密密钥不属于加密密钥例行维护活动。 您可以为了响应对报表服务器的特定威胁来执行这些任务，或者当无法访问报表服务器数据库时作为最后一种解决手段来执行这些任务。  
  
-   当确信现有对称密钥的安全受到威胁时，应重新创建对称密钥。 作为安全性方面的最佳做法，您还可以定期重新创建密钥。  
  
-   当无法还原对称密钥时，应删除现有加密密钥和不可用的加密内容。  
  
## <a name="re-creating-encryption-keys"></a>重新创建加密密钥  
 如果确认对称密钥已泄露给未经授权的用户，或者报表服务器遭到攻击，作为一种防范措施，您想要重置对称密钥，那么可以重新创建对称密钥。 当重新创建对称密钥时，将使用新值对所有加密值重新进行加密。 如果在扩展部署中运行了多个报表服务器，则对称密钥的所有副本都将更新为新值。 报表服务器使用可用的公钥更新部署中每一台服务器的对称密钥。  
  
 只有在报表服务器处于工作状态时，才能重新创建对称密钥。 重新创建加密密钥以及重新对内容进行加密将会中断服务器的操作。 在进行重新加密时，必须将服务器脱机。 在重新加密过程中，不应该向报表服务器发送请求。  
  
 可以使用 Reporting Services 配置工具或 **rskeymgmt** 实用工具重置对称密钥和加密的数据。 有关如何创建对称密钥的详细信息，请参阅[初始化报表服务器（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)。  
  
### <a name="how-to-re-create-encryption-keys-reporting-services-configuration-tool"></a>如何重新创建加密密钥（Reporting Services 配置工具）  
  
1.  通过修改 rsreportserver.config 文件中的 **IsWebServiceEnabled** 属性禁用报表服务器 Web 服务和 HTTP 访问。 此步骤可暂时停止将身份验证请求发送到报表服务器而不会完全关闭服务器。 您必须具有最低限度的服务，以便可以重新创建密钥。  
  
     如果要为报表服务器扩展部署重新创建加密密钥，请对该部署中的所有实例禁用此属性。  
  
    1.  打开 Windows 资源管理器，导航到 *drive*:\Program Files\Microsoft SQL Server\\*report_server_instance*\Reporting Services。 将 *drive* 替换为你的驱动器号，并将 *report_server_instance* 替换为与要禁用其 Web 服务和 HTTP 访问的报表服务器实例对应的文件夹名称。 例如，C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services。  
  
    2.  打开 rsreportserver.config 文件。  
  
    3.  对于 **IsWebServiceEnabled** 属性，指定为 **False**，然后保存所做的更改。  
  
2.  启动 Reporting Services 配置工具，再连接到要配置的报表服务器实例。  
  
3.  在“加密密钥”页上，单击 **“更改”** 。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  重新启动报表服务器 Windows 服务。 如果要为扩展部署重新创建加密密钥，请在所有实例上重新启动该服务。  
  
5.  通过修改 rsreportserver.config 文件中的 **IsWebServiceEnabled** 属性重新启用 Web 服务和 HTTP 访问。 如果使用的是扩展部署，请对所有实例执行此操作。  
  
### <a name="how-to-re-create-encryption-keys-rskeymgmt"></a>如何重新创建加密密钥 (rskeymgmt)  
  
1.  禁用报表服务器 Web 服务和 HTTP 访问。 使用以上过程中的说明停止 Web 服务操作。  
  
2.  在承载报表服务器的计算机上本地运行 **rskeymgmt.exe** 。 使用 **-s** 参数重置对称密钥。 不需要其他参数：  
  
    ```  
    rskeymgmt -s  
    ```  
  
3.  重新启动 Reporting Services Windows 服务。  
  
## <a name="deleting-unusable-encrypted-content"></a>删除无用的加密内容  
 如果由于某些原因无法还原加密密钥，报表服务器将永远无法解密和使用由该密钥加密的所有数据。 若要将报表服务器还原到工作状态，必须删除当前存储在报表服务器数据库中的加密值，然后手动重新指定需要的值。  
  
 删除加密密钥会将所有对称密钥信息从报表服务器数据库中删除，并会删除所有加密内容。 所有未加密的数据都将保持不变；只有加密内容被删除。 删除加密密钥时，报表服务器通过添加新的对称密钥自动对自身进行重新初始化。 删除加密内容时，会出现以下情况：  
  
-   共享数据源中的连接字符串被删除。 运行报表的用户得到错误消息“ConnectionString 属性尚未初始化”。  
  
-   存储的凭据被删除。 报表和共享数据源重新配置为使用所提示的凭据。  
  
-   基于模型（且需要共享数据源配置为使用存储的凭据或不使用凭据）的报表将不会运行。  
  
-   订阅被停用。  
  
 加密内容一旦被删除，便无法恢复。 必须重新指定连接字符串和存储的凭据，并且必须激活订阅。  
  
 可以使用 Reporting Services 配置工具或 **rskeymgmt** 实用工具删除值。  
  
### <a name="how-to-delete-encryption-keys-reporting-services-configuration-tool"></a>如何删除加密密钥（Reporting Services 配置工具）  
  
1.  启动 Reporting Services 配置工具，再连接到要配置的报表服务器实例。  
  
2.  单击 **“加密密钥”** ，再单击 **“删除”** 。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  重新启动报表服务器 Windows 服务。 对于扩展部署，应对所有报表服务器实例执行此操作。  
  
### <a name="how-to-delete-encryption-keys-rskeymmgt"></a>如何删除加密密钥 (rskeymmgt)  
  
1.  在承载报表服务器的计算机上本地运行 **rskeymgmt.exe** 。 必须使用 **-d** 应用参数。 下面的示例说明了必须指定的参数：  
  
    ```  
    rskeymgmt -d  
    ```  
  
2.  重新启动报表服务器 Windows 服务。 对于扩展部署，应对所有报表服务器实例执行此操作。  
  
### <a name="how-to-re-specify-encrypted-values"></a>如何重新指定加密值  
  
1.  对于每个共享数据源，必须重新键入连接字符串。  
  
2.  对于每个使用存储的凭据的报表和共享数据源，必须重新键入用户名和密码，然后再保存。 有关详细信息，请参阅[为报表数据源指定凭据和连接信息](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
3.  对于每个数据驱动订阅，打开每个订阅，再重新键入订阅数据库的凭据。  
  
4.  对于使用加密数据的订阅（其中包括文件共享传递扩展插件和使用加密的任何第三方传递扩展插件），打开每个订阅，再重新键入凭据。 使用报表服务器电子邮件传递的订阅不使用加密数据，因而不受密钥更改的影响。  
  
## <a name="see-also"></a>另请参阅  
 [配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [存储加密的 Report Server 数据（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
