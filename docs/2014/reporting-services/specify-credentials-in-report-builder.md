---
title: 在报表生成器中指定凭据 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7412ce68-aece-41c0-8c37-76a0e54b6b53
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 432b41216418cd1ad1bae70557c95a589f5e78dc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66101143"
---
# <a name="specify-credentials-in-report-builder"></a>在报表生成器中指定凭据
  凭据对试图从数据源中检索数据的用户进行身份验证。 数据源所有者确定必须使用的凭据类型。 例如，数据库管理员可能指定用户必须提供 Windows 用户名和密码。  
  
 在报表定义中，每个数据源定义都指定以下内容：名称、连接字符串、是否使用集成安全性以及当需要凭据但未指定凭据时要显示什么提示。 凭据不保存在报表定义中。 在报表服务器上发布了报表后，数据源可以和报表定义分开进行管理。 数据源所有者可以为报表服务器上的嵌入数据源和共享数据源都指定凭据。  
  
> [!NOTE]  
>  报表服务器管理员必须向用户授予浏览报表服务器的适当权限，以便让其选择共享数据源或模型或者打开或保存报表。 有关详细信息，请参阅[安装、 卸载、 和报表生成器支持](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-when-credentials-are-used"></a>了解何时使用凭据  
 在报表生成器中，在连接到报表服务器或完成数据相关的任务时（例如，创建嵌入数据源，运行数据集查询或预览报表）通常会使用凭据。 凭据不保存在报表中。 将在报表服务器或本地客户端对凭据进行单独管理。 下表介绍了可能需要提供的凭据类型、凭据的存储位置以及使用方法：  
  
-   在 [Reporting Services 登录对话框（报表生成器）](report-builder/reporting-services-login-dialog-box-report-builder.md)中输入的报表服务器凭据。  
  
     当您首次保存到、发布到或浏览到报表服务器或 SharePoint 站点时，可能需要输入凭据。 在报表生成器会话结束之前，将始终使用所输入的凭据。 如果选择保存凭据，则这些凭据将安全地与您的用户设置一起存储在您的计算机上。 在后续的报表生成器会话中，将使用保存的凭据连接到同一报表服务器或 SharePoint 站点。 报表服务器管理员或 SharePoint 管理员指定要使用哪一种类型的凭据。  
  
-   在嵌入数据源的[“数据源属性”对话框 ->“凭据”（报表生成器）](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md)页输入的数据源凭据。  
  
     报表服务器使用这些凭据与外部数据源建立数据连接。 对于某些类型的数据源，可以将凭据安全地存储在报表服务器上。 利用这些凭据，其他用户无需提供凭据即可运行报表进行基础数据连接。  
  
-   运行数据集查询，刷新数据集字段或预览报表时，在[输入数据源凭据对话框（报表生成器）](report-data/enter-data-source-credentials-dialog-box-report-builder.md)中输入的数据源凭据。  
  
     使用这些凭据，报表生成器可以与外部数据源建立数据连接，或对配置为提示需要提供凭据的报表进行预览。 在此对话框中输入的凭据不会存储在报表服务器中，且不能由其他用户使用。 在报表编辑会话期间，报表生成器会对这些凭据进行缓存，以便您无需在每次运行查询或预览报表时输入凭据。  
  
     对于共享数据源，使用 **“保存我的密码”** 选项可以将凭据与用户设置一起保存到本地计算机上。 报表生成器在每次连接到相应的外部数据源时使用保存的凭据。  
  
 有关详细信息，请参阅[“数据源属性”对话框 ->“常规”（报表生成器）](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md)和[在报表生成器中预览报表](report-builder/previewing-reports-in-report-builder.md)。  
  
## <a name="types-of-credentials"></a>凭据类型  
 数据源支持的凭据类型由数据源所有者指定。 例如，若要访问 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库，可能需要提供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登录用户名和密码。 若要访问其他数据源，可能需要提供 Windows 用户名和密码。 某些数据源可能不需要凭据。  
  
### <a name="options-for-specifying-credentials"></a>用于指定凭据的选项  
 下列选项可用于为数据源指定凭据：  
  
-   使用当前的 Windows 用户（也称为集成安全性）。  
  
-   使用存储的用户名和密码。  
  
-   提示用户输入凭据。  
  
-   不需要提供任何凭据。  
  
### <a name="windows-integrated-security"></a>Windows 集成安全性  
 选择 **“使用 Windows 身份验证(集成安全性)”** 时，当前用户的安全令牌传递到数据源。 在这种情况下，系统不会提示用户键入用户名或密码。 此选项通常要求启用委托功能。 如果未启用这些功能，则只能使用此选项访问位于同一台计算机上的数据源。  
  
### <a name="user-name-and-password-login"></a>使用用户名和密码登录  
 选择 **“使用此用户名和密码”** 时，必须提供用户名和密码才能访问数据源。 对于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库，凭据针对的可能是数据库登录。 凭据将传递到数据源用于身份验证。  
  
### <a name="prompted-credentials"></a>提示的凭据  
 指定提示的凭据时，访问该报表的每个用户都必须输入用户名和密码才能检索数据。 建议将此选项用于包含机密数据的报表。 提示的凭据可以对应于 Windows 帐户或数据库登录。 如果数据库服务器未识别出您提供的凭据，或者指定的用户未被授予检索数据的权限，连接将失败。  
  
### <a name="no-credentials"></a>无凭据  
 相应数据源不需要提供凭据。 若要在报表服务器上运行此报表，必须配置无人参与的执行帐户。 有关详细信息，请参阅[配置无人参与的执行帐户&#40;SSRS 配置管理器&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)中[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的文档[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][联机丛书](https://go.microsoft.com/fwlink/?linkid=121312)。  
  
## <a name="see-also"></a>请参阅  
 [安装、 卸载和报表生成器支持](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)   
 [嵌入和共享的数据连接或数据源（报表生成器和 SSRS）](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [报表生成器选项对话框中，设置&#40;报表生成器&#41;](report-builder/set-default-options-for-report-builder.md)   
 [报表生成器中的数据连接、数据源和连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
  
