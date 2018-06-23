---
title: 配置 PowerPivot 无人参与的数据刷新帐户 (PowerPivot for SharePoint) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81401eac-c619-4fad-ad3e-599e7a6f8493
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e80b1ad3323c4cfec76d999cac734cbbb676f5f6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026914"
---
# <a name="configure-the-powerpivot-unattended-data-refresh-account-powerpivot-for-sharepoint"></a>配置 PowerPivot 无人参与的数据刷新帐户 (PowerPivot for SharePoint)
  PowerPivot 无人参与的数据刷新帐户是为在 SharePoint 场中运行 PowerPivot 数据刷新作业而指定的帐户。 通过将其配置，可以使**使用的数据刷新帐户由管理员配置**在数据刷新计划页 （见下文） 中的选项。 如果计划数据刷新的工作簿作者希望使用 PowerPivot 无人参与的数据刷新帐户来运行数据刷新作业，则可以选择此选项。 有关如何查看数据刷新计划中的凭据选项的详细信息，请参阅[计划数据刷新&#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)。  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
 根据配置服务器时选择的选项，可能已创建无人参与的数据刷新帐户。 在默认配置中，无人参与的数据刷新帐户的标识最初将设置为场帐户。 您可以通过更改帐户以便以其他用户身份运行，从而改进部署的安全性。 按照这些说明来更改帐户：[更新凭据使用的现有 PowerPivot 无人参与的数据刷新帐户](#bkmk_editUA)。  
  
 对于所有其他安装情况，您必须使用下面的说明手动配置此帐户。  
  
 本主题包含以下各节：  
  
 [先决条件](#bkmk_prereq)  
  
 [步骤 1： 创建目标应用程序并设置凭据](#bkmk_create)  
  
 [步骤 2： 在 PowerPivot 服务器配置页中指定的无人参与的帐户](#bkmk_specifyUA)  
  
 [步骤 3： 授予参与对帐户的权限](#bkmk_grant)  
  
 [步骤 4： 授予读取权限，才能访问数据刷新中使用的外部数据源](#bkmk_dbread)  
  
 [步骤 5： 验证数据中的帐户可用性刷新配置页](#bkmk_verify)  
  
 [使用 PowerPivot 无人参与的数据刷新帐户](#bkmk_use)  
  
 [更新凭据使用的现有 PowerPivot 无人参与的数据刷新帐户](#bkmk_editUA)  
  
##  <a name="bkmk_prereq"></a> 先决条件  
 必须启用和配置 Secure Store Service，并且必须生成主密钥。 有关如何执行此操作的说明，请参阅[使用 SharePoint 2010 的 PowerPivot 数据刷新](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
 您必须提前确定哪一 Windows 域用户帐户用作 PowerPivot 无人参与的数据刷新帐户。 该帐户应该是为此目的而专门创建的帐户，以便您可以监视其使用方式。  
  
 您必须知道 PowerPivot 系统服务的应用程序标识。 你将提供此服务帐户**完全控制**权限通过无人参与的数据刷新帐户，当在步骤 1 中创建它的目标应用程序。 这些权限允许 PowerPivot 系统服务在数据刷新过程中检索无人参与的数据刷新帐户的凭据。 若要获取所需的服务帐户信息，请打开**配置服务帐户**页在管理中心中，选择使用 PowerPivot 服务应用程序的服务应用程序池。 默认情况下，这是**服务应用程序池-SharePoint Web 服务系统**。  
  
## <a name="configure-the-unattended-powerpivot-data-refresh-account"></a>配置无人参与的 PowerPivot 数据刷新帐户。  
 对于每个 PowerPivot 服务应用程序，您只能配置一个 PowerPivot 无人参与的数据刷新帐户。 帐户信息存储于目标应用程序中设置为预定义的 Windows 域用户帐户的 Secure Store Service 中。 一旦创建目标应用程序后，您可以在 PowerPivot 服务应用程序的配置页中将其指定为 PowerPivot 数据刷新帐户。  
  
> [!NOTE]  
>  在基于无人参与的数据刷新帐户执行数据刷新时，对于用于无人参与的数据刷新的 Windows 用户帐户记录，将记录其使用情况报告和数据刷新历史记录。 如果您要求对请求数据刷新或拥有计划的个体的更精确记录，则考虑用于运行数据刷新的其他选项之一。 也就是说，让用户指定自己的凭据（这是默认设置）或者创建其他目标应用程序以便存储要用于数据刷新的任何 Windows 凭据。 有关详细信息，请参阅[为 PowerPivot 数据刷新配置存储凭据&#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
 创建无人参与的数据刷新帐户包括五个部分。  
  
-   在 Secure Store Service 中创建目标应用程序并指定凭据。  
  
-   在 PowerPivot 服务器配置页中为无人参与的数据刷新帐户指定目标应用程序 ID。  
  
-   对该帐户授予“参与讨论”权限。  
  
-   授予该帐户读取权限以便在数据刷新过程中访问外部数据源。  
  
-   验证该帐户在已发布的 PowerPivot 工作簿的“管理数据刷新计划”页中可用。  
  
###  <a name="bkmk_create"></a> 步骤 1： 创建目标应用程序并设置凭据  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  单击**Secure Store Service**。  
  
3.  在管理目标应用程序中，单击**新建**。  
  
4.  目标应用程序 ID，在键入**PowerPivotDataRefresh**。  
  
5.  在显示名称键入**PowerPivot 数据刷新**。  
  
6.  在“联系人电子邮件”中，键入您的电子邮件地址。  
  
7.  在目标应用程序类型，选择**单个**。  
  
    > [!NOTE]  
    >  指定“单独”帐户类型适合于此情况，因为只有 PowerPivot 服务应用程序将请求 PowerPivot 无人参与的数据刷新帐户的凭据。 实际上，该服务应用程序是无人参与的数据刷新帐户的唯一用户，这使得“单独”帐户类型成为此目标应用程序的最佳选择。  
  
8.  跳过“目标应用程序页 URL”。 PowerPivot 数据刷新不会使用它。  
  
9. 单击“下一步” 。  
  
10. 在**指定安全存储区目标应用程序的凭据字段**页上，接受默认值。 字段名称和类型应该是 Windows 用户名和 Windows 密码  
  
11. 单击“下一步” 。  
  
12. 在“目标应用程序管理员”中，指定 PowerPivot 服务应用程序的应用程序池标识。 该服务需要**完全控制**权限以便它可以检索无人参与的数据刷新在运行时的帐户信息。 此外，指定应该对应用程序设置具有管理权限的任何其他 SharePoint 用户的 Windows 域用户帐户。  
  
13. 单击“确定” 。  
  
14. 选择你刚刚创建的目标应用程序，单击向下箭头并选择**设置凭据。**  
  
15. 在**凭据所有者**，键入你想要有权更新凭据的 Windows 域用户帐户。 有关数据刷新操作使用的凭据和**凭据所有者**有权修改的凭据。  
  
16. 单击“确定” 。  
  
###  <a name="bkmk_specifyUA"></a> 步骤 2： 在 PowerPivot 服务器配置页中指定的无人参与的帐户  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  找到 PowerPivot 服务应用程序。 您可以通过类型来确定服务应用程序。 PowerPivot 服务应用程序的类型为 **“PowerPivot 服务应用程序”**。  
  
3.  单击 PowerPivot 服务应用程序名称。 等待 PowerPivot 管理面板出现。  
  
4.  在操作，在右上角，单击**配置服务应用程序设置**。  
  
5.  在数据刷新，PowerPivot 无人参与数据刷新帐户中，键入你在上一步中创建目标应用程序 ID: **PowerPivotDataRefresh**。  
  
6.  单击“确定” 。  
  
###  <a name="bkmk_grant"></a> 步骤 3： 授予参与对帐户的权限  
 在您可以使用 PowerPivot 无人参与的数据刷新帐户之前，对于使用该帐户的任何 PowerPivot 工作簿，必须授予“参与讨论”权限。 此权限级别是从库中打开工作簿、然后在刷新数据后将其保存回库中所必需的。  
  
 分配权限这个步骤将由网站集管理员来执行。 SharePoint 权限可以在根网站集或其下的任何级别分配，包括单独的文档和项。 设置权限的方式将因您所需的粒度而异。 下面的步骤说明可用于授予权限的一个方法。  
  
1.  在 SharePoint 站点上，在站点操作，单击**站点权限**。  
  
2.  单击 **“授予权限”**。  
  
3.  在“选择用户”中，键入您指派为 PowerPivot 无人参与的帐户的 Windows 域用户帐户。 这是在 Secure Store Service 的目标应用程序中指定的 Windows 域用户帐户的名称。  
  
4.  在授予权限，选择**直接向用户授予权限**。  
  
5.  选择**参与讨论**，然后单击**确定**。  
  
###  <a name="bkmk_dbread"></a> 步骤 4： 授予读取权限，才能访问数据刷新中使用的外部数据源  
 在将数据导入到某一 PowerPivot 工作簿时，与外部数据的连接常常基于可信连接或者使用当前用户标识来连接到数据源的模拟连接。 只有在当前用户有权读取其导入的数据时，这些连接类型才有效。  
  
 在数据刷新方案中，现在将重复使用过去用于导入数据的相同连接字符串来刷新数据。 如果该连接字符串假定当前用户（例如，包含 Integrated_Security=SSPI 的字符串），则 PowerPivot 系统服务会将 PowerPivot 无人参与的数据刷新帐户的用户标识作为当前用户传递。 只有在 PowerPivot 无人参与的数据刷新帐户对外部数据源具有读取权限时，此连接才会成功。  
  
 因此，您必须向 PowerPivot 无人参与的数据刷新帐户授予相应的只读权限，使此帐户能够以只读方式访问在该无人参与的帐户下运行的任何数据刷新操作中使用的所有外部数据源。  
  
 如果您是组织中使用的数据源的管理员，则可以创建一个登录名，然后分配必需的权限。 否则，您必须与数据所有者联系并且提供帐户信息。 请确保指定映射到 PowerPivot 无人参与的数据刷新帐户的 Windows 域用户帐户。 这是您在本主题的“（步骤 1）：创建目标应用程序并且设置凭据”中指定的帐户。  
  
###  <a name="bkmk_verify"></a> 步骤 5： 验证数据中的帐户可用性刷新配置页  
  
1.  打开包含 PowerPivot 数据的已发布工作簿的数据刷新配置页。 有关如何打开的页的说明，请参阅[计划数据刷新&#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)。  
  
2.  验证**使用的数据刷新帐户由管理员配置**选项启用数据刷新配置页中。  
  
3.  选择**也尽快刷新**复选框，然后单击**确定**。  
  
4.  在库中包含的工作簿，选择工作簿，单击显示右侧的向下箭头，然后选择**管理 PowerPivot 数据刷新**。 如果数据刷新作业正在返回大量数据，您可能需要等待几分钟。  
  
 如果发生错误，则可以单击**配置计划**在数据刷新历史记录页后，可以尝试不同的凭据。 您还可能需要检查原始工作簿中的数据源连接信息，以便查看在数据刷新过程中使用的连接字符串。 该连接字符串将提供与您可用于解决问题的服务器位置和数据库有关的信息。  
  
 有关疑难解答的详细信息，请参阅[解决 PowerPivot 数据刷新](http://go.microsoft.com/fwlink/p/?LinkID=223279)TechNet Wiki 上。  
  
##  <a name="bkmk_use"></a> 使用 PowerPivot 无人参与的数据刷新帐户  
 在 PowerPivot 数据刷新计划页上的三个凭据选项中，只有第一个选项与无人参与的数据刷新帐户相关。 在设置数据刷新计划时，请务必选择此选项。  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 不要使用第三个凭据选项（要求您输入目标应用程序 ID 的选项）来访问 PowerPivot 无人参与的数据刷新帐户。 因为使用该选项会执行一个附加的模拟检查，如果您尝试将其与 PowerPivot 无人参与的数据刷新帐户（或者基于“单独”帐户类型的任何目标应用程序）一起使用，将会导致验证错误。 有关如何使用第三个选项的详细信息，请参阅[为 PowerPivot 数据刷新配置存储凭据&#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
##  <a name="bkmk_editUA"></a> 更新凭据使用的现有 PowerPivot 无人参与的数据刷新帐户  
 如果无人参与的数据刷新帐户已通过安装程序配置或者已由管理员配置，则您可以通过编辑存储凭据的目标应用程序，更新用户名或密码。 请注意，当您在 Secure Store Service 中编辑凭据时，以前与 PowerPivot 无人参与的数据刷新帐户相关联的原始 Windows 标识将不可见。 无论您是更新到期的密码还是指定不同帐户，都必须始终在 Secure Store Service 中为该目标应用程序重新键入用户名和密码。  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  单击**Secure Store Service**。  
  
3.  选中的复选框旁边**PowerPivotDataRefresh**。  
  
4.  在凭据单击**设置**。  
  
5.  在**凭据所有者**，键入你想要有权更新凭据的 Windows 域用户帐户。 有关数据刷新操作使用的凭据和**凭据所有者**有权修改的凭据。  
  
6.  在“用户名”中，键入将成为无人参与的数据刷新凭据的一部分的 Windows 域用户帐户。  
  
7.  在“密码”中，键入该帐户的密码，然后重新键入以确认该密码。  
  
8.  单击“确定” 。  
  
 如果您不仅要更改密码，也要更改帐户用户名，则很可能需要执行附加的配置步骤，例如向外部数据源授予读取权限和 SharePoint 权限以便更新 PowerPivot 工作簿。 有关说明，请转到 PowerPivot 无人参与的数据刷新帐户配置中的此步骤：[步骤 3： 授予参与的帐户权限](#bkmk_grant)，然后继续结束带有验证的所有剩余的步骤，帐户配置正确。  
  
## <a name="see-also"></a>请参阅  
 [使用 SharePoint 2010 的 PowerPivot 数据刷新](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [计划数据刷新&#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [PowerPivot 数据刷新](power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  