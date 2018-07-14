---
title: 创建和管理共享的数据源 (SharePoint 集成模式下的 Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], shared data sources
- shared data sources [Reporting Services]
ms.assetid: 2d3428e4-a810-4e66-a287-ff18e57fad76
caps.latest.revision: 12
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d75ac29d1136106d88022bb8c5e3fd66e62124c0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194767"
---
# <a name="create-and-manage-shared-data-sources-reporting-services-in-sharepoint-integrated-mode"></a>创建和管理共享数据源（SharePoint 集成模式下的 Reporting Services）
  从 SharePoint 库运行报表时，可以在报表或链接至报表的外部文件中定义连接信息。 如果连接信息嵌入在报表中，则该信息称为自定义数据源。 如果连接信息在外部文件中进行定义，则该信息称为共享数据源。 外部文件可以是报表服务器数据源 (.rsds) 文件，也可以是 Office 数据连接 (.odc) 文件。  
  
 .rsds 文件与 .rds 文件类似，但它具有不同的架构。 若要创建 .rsds 文件，可以从报表设计器或模型设计器向 SharePoint 库发布一个 .rds 文件（将从该原始 .rds 文件创建一个新的 .rsds 文件）。 也可以在 SharePoint 站点上的库中创建新文件。  
  
 在创建或发布共享数据源后，可以编辑连接属性或者在不再使用共享数据源时删除此文件。 删除共享数据源之前，您应该确定是否有报表和报表模型在使用该数据源。 可以通过查看引用共享数据源的依赖项来进行确定。  
  
 虽然依赖项列表会告诉您是否引用了共享数据源，但它不会告诉您数据源是否正在使用。 若要确定共享数据源或模型是否正在使用，您可以在报表服务器计算机上查看日志文件。 如果您无权访问日志文件，或者这些文件不包含您想要的信息，请考虑在确定报表的实际状态时将其移动到不可访问的文件夹。  
  
### <a name="to-create-a-shared-data-source-rsds-file-sharepoint-2010"></a>创建共享数据源 (.rsds) 文件 (SharePoint 2010)  
  
1.  在库功能区上单击 **“文档”** 选项卡。  
  
2.  在 **“新建文档”** 菜单上，单击 **“报表数据源”**。  
  
    > [!NOTE]  
    >  如果在菜单上没有看到 **“报表数据源”** 项，说明报表数据源内容类型尚未启用。 有关详细信息，请参阅[将报表服务器内容类型添加到库&#40;在 SharePoint 集成模式下的 Reporting Services&#41;](../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  
3.  在 **“名称”** 中，为 .rsds 文件输入一个说明性名称。  
  
4.  在 **“数据源类型”** 中，从列表中选择数据源的类型。 有关详细信息，请参阅 [Reporting Services 支持的数据源 (SSRS)](create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
5.  在 **“连接字符串”** 中，指定指向数据源的指针和建立外部数据源连接所必需的任何其他设置。 您所使用的数据源类型决定了连接字符串的语法。 有关详细信息和示例，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
6.  在 **“凭据”** 中，指定报表服务器如何获取访问外部数据源的凭据。 凭据可通过存储、提示、集成或配置方式用于无人参与的报表处理。  
  
    -   若要使用打开报表的用户凭据访问数据，请选择“Windows 身份验证(集成)”。 如果 SharePoint 站点或场使用窗体身份验证或通过可信帐户连接至报表服务器，请不要选择此选项。 若要为此报表计划订阅或数据处理，请不要选择此选项。 如果您的域启用了 Kerberos 身份验证或者数据源与报表服务器位于同一台计算机上，则此选项最为有效。 如果未启用 Kerberos 身份验证，则只能将 Windows 凭据传递到另一台计算机。 也就是说，如果外部数据源位于需要另行连接的其他计算机上，则会出现错误而不会获得期望的数据。  
  
    -   若要使用户在每次运行报表时都输入其凭据，请选择 **“凭据提示”** 。 若要为此报表计划订阅或数据处理，请不要选择此选项。  
  
    -   若要使用一组凭据访问数据，请选择 **“已存储凭据”** 。 凭据在存储之前是加密的。 您可以选择用于确定如何对已存储凭据进行身份验证的选项。 如果已存储的凭据属于 Windows 用户帐户，请选择“用作 Windows 凭据”。 如果要设置数据库服务器的执行上下文，请选择 **“设置此帐户的执行上下文”** 。 有关[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库，此选项将设置 SETUSER 函数。 有关详细信息，请参阅 [SETUSER (Transact-SQL)](/sql/t-sql/statements/setuser-transact-sql)。  
  
    -   如果要在连接字符串中指定凭据，或者如果要使用在报表服务器上配置的最低特权帐户运行报表，请选择“不需要提供凭据”。 如果未在报表服务器上配置此帐户，系统将提示用户输入凭据，并且不会运行您为报表定义的任何计划操作。  
  
7.  如果您想要数据源处于活动状态，则选择 **“启用此数据源”** 。 如果配置了数据源但该数据源未处于活动状态，则在用户尝试基于该数据源使用某一报表时，系统将会显示错误消息。  
  
8.  单击 **“测试连接”** 按钮可验证数据源配置。  
  
    > [!NOTE]  
    >  对于 XML 数据源类型，不支持“测试连接”按钮。  
  
9. 单击 **“确定”** 保存共享的数据源。  
  
### <a name="to-view-dependent-items"></a>若要查看依赖项  
  
1.  打开包含 .rsds 文件的库。  
  
2.  指向共享数据源。  
  
3.  单击以显示向下箭头，然后选择 **“查看依赖项”**。  
  
     对于报表模型，依赖项列表将显示在报表生成器中创建的报表。 对于共享数据源，依赖项列表可以包括报表和报表模型。  
  
### <a name="to-delete-a-shared-data-source-rsds-file"></a>删除共享数据源 (.rsds) 文件  
  
1.  打开包含 .rsds 文件的库。  
  
2.  指向共享数据源。  
  
3.  单击以显示向下箭头，然后单击 **“删除”**。  
  
 如果错删了要保留的共享数据源，则可以创建一个包含相同连接信息的新共享数据源。 重新创建共享数据源后，必须打开使用该数据源的每个报表和模型，并选择该共享数据源。 新的共享数据源项可以有不同于已删除数据源的名称、凭据或连接字符串语法。 在连接解析到相同数据源时，数据源属性可能与原始值不同。  
  
 删除报表模型时要特别小心。 如果删除模型，则将无法在报表生成器中打开和修改任何基于该模型的报表。 如果由于疏忽删除了现有报表使用的模型，则必须重新生成该模型、重新创建和保存使用该模型的任何报表，并重新指定要使用的任何模型项安全性。 不能仅重新生成模型然后将其附加到现有报表。  
  
## <a name="see-also"></a>请参阅  
 [为报表数据源指定凭据和连接信息](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
