---
title: 从 SharePoint 站点更新报表数据源的凭据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e0c50b6e-89e7-4b4d-8fe5-c90682c5d1b1
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 324b8730b4a61fdca6f0d1bafae27c6ca056f594
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128931"
---
# <a name="update-credentials-in-report-data-sources-from-a-sharepoint-site"></a>从 SharePoint 站点更新报表数据源的凭据
  本主题介绍如何更新报表中嵌入的数据源和保存在 SharePoint 文档库中的共享数据源。  
  
 许多报表可能包含数据源或使用配置为使用 Windows 身份验证的共享数据源。 在某些情况下（如在保存到 SharePoint 文档库的报表上创建数据警报），您需要将数据源凭据更新到存储的凭据或不需要凭据。  
  
 若要在报表中使用存储的凭据，您可能会决定创建并使用一个新的 SQL Server 登录名。 有关详细信息，请参阅 [创建登录名](../../relational-databases/security/authentication-access/create-a-login.md)。  
  
### <a name="to-update-an-embedded-data-source-to-use-stored-credentials"></a>更新嵌入的数据源以使用存储的凭据  
  
1.  转到保存该报表的 SharePoint 文档库。  
  
2.  单击针对该报表展开下拉菜单的图标，然后单击“管理数据源”。  
  
     此时将打开“管理数据源”页。  
  
3.  在 **“名称”** 列中，单击该数据源。  
  
4.  针对 **“连接类型”** ，确认已选中 **“自定义数据源”** 选项。  
  
     此选项指示数据源嵌入在报表中。  
  
5.  保留 **“数据源类型”** 和 **“连接字符串”** 选项不变，除非您要将报表连接到其他类型的数据源、其他服务器或数据存储区。  
  
6.  对于 **“凭据”**，请选择 **“存储的凭据”**。 仅当数据源不接受凭据，或者要通过其他方式传递凭据时，才使用此选项。  
  
     **“不需要凭据”** 选项也可以在某些情况下使用。  
  
     对于某些数据源类型，必须在报表服务器上配置无人参与的执行帐户。 有关详细信息，请参阅[从外部数据源中添加数据 (SSRS)](add-data-from-external-data-sources-ssrs.md)和[配置无人参与的执行帐户（SSRS 配置管理器）](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)中相应的数据源类型的主题。  
  
7.  键入用户名和密码。  
  
    -   如果帐户是 Windows 域用户帐户，请按照以下格式指定该帐户：\<域>\\<帐户\>，然后选择“在与数据源建立连接时用作 Windows 凭据”。  
  
    -   如果用户名和密码是数据库凭据，请不要选择 **“在与数据源建立连接时用作 Windows 凭据”**。 如果数据库服务器支持模拟或委托，则可选择 **“设置此帐户的执行上下文”**。  
  
8.  若要验证数据源是否可以使用更新的凭据进行连接，请单击 **“测试连接”**。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-update-a-shared-data-source-to-use-stored-credentials"></a>更新共享的数据源以使用存储的凭据  
  
1.  转到保存共享数据源的 SharePoint 文档库。  
  
2.  单击针对共享数据源展开下拉菜单的图标，然后单击“编辑数据源定义”。  
  
     将打开“数据源”页。  
  
3.  保留 **“数据源类型”** 和 **“连接字符串”** 选项不变，除非您要将共享数据源连接到其他类型的数据源、其他服务器或数据存储区。  
  
4.  对于 **“凭据”**，请选择 **“存储的凭据”**。  
  
     **“不需要凭据”** 选项也可以在某些情况下使用。 仅当数据源不接受凭据，或者要通过其他方式传递凭据时，才使用此选项。  
  
     对于某些数据源类型，必须在报表服务器上配置无人参与的执行帐户。 有关详细信息，请参阅[从外部数据源中添加数据 (SSRS)](add-data-from-external-data-sources-ssrs.md)和[配置无人参与的执行帐户（SSRS 配置管理器）](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)中相应的数据源类型的主题。  
  
5.  键入用户名和密码。  
  
    -   如果帐户是 Windows 域用户帐户，请按照以下格式指定该帐户：\<域>\\<帐户\>，然后选择“在与数据源建立连接时用作 Windows 凭据”。  
  
    -   如果用户名和密码是数据库凭据，请不要选择 **“在与数据源建立连接时用作 Windows 凭据”**。 如果数据库服务器支持模拟或委托，则可选择 **“设置此帐户的执行上下文”**。  
  
6.  若要验证数据源是否可以使用更新的凭据进行连接，请单击 **“测试连接”**。  
  
7.  验证是否选择了启用此数据源。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [将文档上传到 SharePoint 库（SharePoint 模式下的 Reporting Services）](../upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
  