---
title: 创建、修改和删除共享数据源 (SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- modifying data source properties
- shared data sources [Reporting Services]
- removing shared data sources
- roles [Reporting Services], shared data sources
- data sources [Reporting Services], shared
- data sources [Reporting Services], modifying properties
- deleting shared data sources
ms.assetid: 1e58c1c2-5ecf-4ce6-9d04-0a8acfba17be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1045f9a0c271ee4c3befe434a3eef50f0edee6df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573209"
---
# <a name="create-modify-and-delete-shared-data-sources-ssrs"></a>创建、修改和删除共享数据源 (SSRS)
  共享数据源是一组可供在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器上运行的多个报表、模型和数据驱动订阅引用的数据源连接属性。  共享数据源为随时间推移经常发生变化的数据源属性的管理提供了一种简单的方法。 如果用户帐户或密码发生更改，或者如果将数据库移到其他服务器，则可在一个位置对连接信息进行更新。  
  
 对于报表和数据驱动订阅，共享数据源是可选的，但对于报表模型，共享数据源是必需的。 如果计划将报表模型用于特别报告，则必须创建和维护一个共享数据源项才能为此模型提供连接信息。  
  
 共享数据源由以下几个部分组成：  
  
|组成部分|描述|  
|----------|-----------------|  
|“属性”|名称用于在报表服务器文件夹层次结构中标识该项。|  
|描述|查看文件夹的内容时，在 Web 门户中与该项一起出现的说明。|  
|连接类型|与数据源一起使用的数据处理扩展插件。 您只能使用部署在报表服务器上的数据处理扩展插件。 有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 附带的数据处理扩展插件的详细信息，请参阅 [Reporting Services 支持的数据源 (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。|  
|连接字符串|数据库的连接字符串。 有关详细信息和常用数据源的连接字符串示例，请参阅 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。|  
|凭据类型|指定如何为连接获取凭据以及在建立连接后是否使用这些凭据。 有关详细信息，请参阅[为报表数据源指定凭据和连接信息](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).|  
  
 共享数据源不包含用于检索数据的查询信息。 查询始终保存在报表定义中。  
  
## <a name="creating-and-modifying-shared-data-sources"></a>创建和修改共享数据源  
 若要创建共享数据源或修改其属性，必须对报表服务器拥有 **管理数据源** 的权限。 如果报表服务器在本机模式下运行，则可在 Web 门户中创建和配置共享数据源。 如果报表服务器在 SharePoint 集成模式下运行，则可使用 SharePoint 站点上的应用程序页。 对于任何报表服务器，不管其模式如何，均可在报表设计器中创建共享数据源，然后将该数据源发布到目标服务器。  
  
 在报表服务器上创建共享数据源后，可通过创建角色分配来控制对该共享数据源的访问、将该共享数据源移到其他位置、对其重命名，或使之脱机以防止在对外部数据源执行维护操作时处理报表。 如果您在报表服务器文件夹层次结构中对共享数据源项重命名，或将其移到其他位置，则引用该共享数据源的所有报表或订阅中的路径信息都会相应更新。 如果使共享数据源脱机，则直到您重新启用该数据源后所有报表、模型和订阅才会运行。  
  
 有关如何控制对报表服务器文件夹层次结构中的共享数据源的访问的详细信息，请参阅 [保护共享数据源项](../../reporting-services/security/secure-shared-data-source-items.md)。  
  
 **在报表设计器中创建共享数据源**  
  
1.  在“报表数据”窗格的工具栏中，单击 **“新建”** ，然后单击 **“数据源”** 。 此时将打开 **“数据源属性”** 对话框。  
  
    > [!NOTE]  
    >  如果“报表数据”窗格不可见，请单击“视图”  菜单上的“报表数据”  。  
  
2.  在 **“名称”** 文本框中，键入数据源的名称，或接受默认值。 此数据源名称在报表内部使用。 为便于识别，建议数据源名称包含在连接字符串中指定的数据库的名称。  
  
3.  确认是否已选中“使用共享数据源引用”  ，然后执行以下操作。  
  
    1.  单击 **“新建”** 。 在 **“共享数据源属性”** 对话框中，执行步骤 2 和 3 创建新数据源。  
  
    2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
         解决方案资源管理器的“共享数据源”文件夹中将显示新的共享数据源。  
  
4.  单击 **“凭据”** 。  
  
     指定用于此数据源的凭据。 数据源所有者将选择支持的凭据类型。  
  
 **在 Web 门户中创建共享数据源**  
  
1.  在 Web 门户中，选择“新建”   > “数据源”  。 
  
4.  为相应项键入一个名称。 名称必须包含至少一个字符并且必须以字母开头。 它也可以包括特定的一些符号，但不能包括空格或以下字符：; ? : \@ & = + , $ / * < > | " /。  
  
5.  根据需要键入说明，向用户提供相关的连接信息。  
  
6.  在 **“数据源类型”** 列表中，指定用于处理来自数据源的数据的数据处理扩展插件。  
  
7.  对于 **“连接字符串”** ，指定报表服务器用于连接数据源的连接字符串。 建议不要在连接字符串中指定凭据。  
  
     以下示例演示用于连接到本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AdventureWorks2016 数据库的连接字符串：  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2016 
    ```  
  
8.  对于 **“连接方式”** ，请指定在报表运行时获取凭据的方式：  
  
    -   如果希望提示用户输入登录名和密码，请单击 **“运行该报表的用户提供的凭据”** 。 若要将用户输入的凭据作为 Windows 凭据，请单击 **“在与数据源建立连接时用作 Windows 凭据”** 。 如果用户名和密码是数据库凭据，则不选择此选项。  
  
    -   如果要将该数据源用作共享数据源以及使用由数据源所有者管理的已保存凭据，或者将该数据源用于支持订阅或其他计划操作（例如自动生成报表历史记录）的报表，请单击“安全存储在报表服务器中的凭据”  。 如果数据库服务器支持模拟或委托，则可以选择 **“与数据源建立连接之后模拟经过身份验证的用户”** 。  
  
    -   如果希望报表服务器将访问报表的用户的凭据传递给承载外部数据源的服务器，请单击 **“Windows 集成安全性”** 。 在这种情况下，系统不会提示用户键入用户名或密码。  
  
    -   如果数据源不使用凭据（例如，如果数据源是通过文件系统访问的 XML 文件），请单击“不需要凭据”  。 仅当此凭据类型对于相应数据源有效时，才能指定它。 如果为要求身份验证的数据源选择此选项，则连接将失败。 如果选择此选项，请确保配置无人参与的执行帐户，以便在用户凭据不可用时，报表服务器可连接到其他计算机以检索数据或文件。  
  
         有关配置凭据的详细信息，请参阅 [指定报表数据源的凭据和连接信息](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)。 有关无人参与的执行帐户的详细信息，请参阅[配置无人参与的执行帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
9. 单击 **“测试连接”** 按钮可验证数据源配置。  
  
    > [!NOTE]  
    >  对于 XML 数据源类型，不支持“测试连接”按钮。  
  
10. 单击 **“确定”** 。  
  
 **在 Web 门户中修改共享数据源**  
  
1.  在 Web 门户中，导航到共享数据源。  
  
2.  选择共享数据源右上角的省略号 (...) >“管理”  。   

    **“属性”** 页将打开。
  
3.  修改数据源，再单击 **“应用”** 。  
  
## <a name="deleting-shared-data-sources"></a>删除共享数据源  
 可使用与从报表服务器删除任何项完全相同的方式来删除共享数据源。  
  
 **删除共享数据源**  
  
1. 在 Web 门户中，导航到共享数据源。  
  
2.  选择共享数据源右上角的省略号 (...) >“管理”  。    
    **“属性”** 页将打开。
  
3. 单击 **“删除”** ，再单击 **“确定”** 。  
  
删除共享数据源会停用使用该共享数据源的任何报表、模型或数据驱动订阅。 在没有数据源连接信息的情况下，这些项将不再运行。 若要激活这些项，必须打开每一项并执行以下操作：  
  
-   对于引用共享数据源的报表和数据驱动订阅，可在报表属性或订阅中指定数据源连接信息，或者选择具有要使用的值的新共享数据源。  
  
-   对于模型和使用该模型的报表生成器报表，必须指定新的共享数据源。 模型只能通过共享数据源获取数据源连接信息。  
  
 删除共享数据源后没有“撤消”操作可用。 不过，如果您意外删除了一个共享数据源，则可以使用与删除的共享数据源相同的属性值来创建一个新的共享数据源。 您必须打开每个报表、模型和数据驱动订阅才能将该共享数据源重新绑定到使用该共享数据源的项，但是只要这些数据源属性和以前的数据源属性相同，这些报表、模型和订阅便可像以前一样正常使用。  
  
## <a name="importing-shared-data-sources"></a>导入共享数据源  

**在报表设计器中导入现有数据源**  
  
1.  在解决方案资源管理器中，右键单击报表服务器项目中的“共享数据源”  文件夹，然后单击“添加现有项”  。 此时将打开 **“添加现有项”** 对话框。  
  
2.  导航到一个现有报表定义共享数据源 (rds) 文件，然后单击“打开”  。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="shared-data-sources-in-sharepoint"></a>SharePoint 中的共享数据源  
 从 SharePoint 库运行报表时，可以在报表或链接至报表的外部文件中定义连接信息。 如果连接信息嵌入在报表中，则该信息称为自定义数据源。 如果连接信息在外部文件中进行定义，则该信息称为共享数据源。 外部文件可以是报表服务器数据源 (.rsds) 文件，也可以是 Office 数据连接 (.odc) 文件。  
  
 .rsds 文件与 .rds 文件类似，但它具有不同的架构。 若要创建 .rsds 文件，可以从报表设计器或模型设计器向 SharePoint 库发布一个 .rds 文件（将从该原始 .rds 文件创建一个新的 .rsds 文件）。 也可以在 SharePoint 站点上的库中创建新文件。  
  
 在创建或发布共享数据源后，可以编辑连接属性或者在不再使用共享数据源时删除此文件。 删除共享数据源之前，您应该确定是否有报表和报表模型在使用该数据源。 可以通过查看引用共享数据源的依赖项来进行确定。  
  
 虽然依赖项列表会告诉您是否引用了共享数据源，但它不会告诉您数据源是否正在使用。 若要确定共享数据源或模型是否正在使用，您可以在报表服务器计算机上查看日志文件。 如果您无权访问日志文件，或者这些文件不包含您想要的信息，请考虑在确定报表的实际状态时将其移动到不可访问的文件夹。  
  
 **创建共享数据源 (.rsds) 文件 (SharePoint 2010)**  
  
1.  在库功能区上单击 **“文档”** 选项卡。  
  
2.  在 **“新建文档”** 菜单上，单击 **“报表数据源”** 。  
  
    > [!NOTE]  
    >  如果在菜单上没有看到 **“报表数据源”** 项，说明报表数据源内容类型尚未启用。 有关详细信息，请参阅 [向 SharePoint 库添加 Reporting Services 内容类型](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  
3.  在 **“名称”** 中，为 .rsds 文件输入一个说明性名称。  
  
4.  在 **“数据源类型”** 中，从列表中选择数据源的类型。 有关详细信息，请参阅 [Reporting Services 支持的数据源 (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
5.  在 **“连接字符串”** 中，指定指向数据源的指针和建立外部数据源连接所必需的任何其他设置。 您所使用的数据源类型决定了连接字符串的语法。 有关详细信息和示例，请参阅 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
6.  在 **“凭据”** 中，指定报表服务器如何获取访问外部数据源的凭据。 凭据可通过存储、提示、集成或配置方式用于无人参与的报表处理。  
  
    -   若要使用打开报表的用户凭据访问数据，请选择“Windows 身份验证(集成)”  。 如果 SharePoint 站点或场使用窗体身份验证或通过可信帐户连接至报表服务器，请不要选择此选项。 若要为此报表计划订阅或数据处理，请不要选择此选项。 如果您的域启用了 Kerberos 身份验证或者数据源与报表服务器位于同一台计算机上，则此选项最为有效。 如果未启用 Kerberos 身份验证，则只能将 Windows 凭据传递到另一台计算机。 也就是说，如果外部数据源位于需要另行连接的其他计算机上，则会出现错误而不会获得期望的数据。  
  
    -   若要使用户在每次运行报表时都输入其凭据，请选择 **“凭据提示”** 。 若要为此报表计划订阅或数据处理，请不要选择此选项。  
  
    -   若要使用一组凭据访问数据，请选择 **“已存储凭据”** 。 凭据在存储之前是加密的。 您可以选择用于确定如何对已存储凭据进行身份验证的选项。 如果已存储的凭据属于 Windows 用户帐户，请选择“用作 Windows 凭据”。 如果要设置数据库服务器的执行上下文，请选择 **“设置此帐户的执行上下文”** 。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，此选项将设置 SETUSER 函数。 有关详细信息，请参阅 [SETUSER (Transact-SQL)](../../t-sql/statements/setuser-transact-sql.md)。  
  
    -   如果要在连接字符串中指定凭据，或者如果要使用在报表服务器上配置的最低特权帐户运行报表，请选择“不需要提供凭据”  。 如果未在报表服务器上配置此帐户，系统将提示用户输入凭据，并且不会运行您为报表定义的任何计划操作。  
  
7.  如果您想要数据源处于活动状态，则选择 **“启用此数据源”** 。 如果配置了数据源但该数据源未处于活动状态，则在用户尝试基于该数据源使用某一报表时，系统将会显示错误消息。  
  
8.  单击 **“测试连接”** 按钮可验证数据源配置。  
  
    > [!NOTE]  
    >  对于 XML 数据源类型，不支持“测试连接”按钮。  
  
9. 单击 **“确定”** 保存共享的数据源。  
  
 **删除共享数据源 (.rsds) 文件**  
  
1.  打开包含 .rsds 文件的库。  
  
2.  指向共享数据源。  
  
3.  单击以显示向下箭头，然后单击 **“删除”** 。  
  
 如果错删了要保留的共享数据源，则可以创建一个包含相同连接信息的新共享数据源。 重新创建共享数据源后，必须打开使用该数据源的每个报表和模型，并选择该共享数据源。 新的共享数据源项可以有不同于已删除数据源的名称、凭据或连接字符串语法。 在连接解析到相同数据源时，数据源属性可能与原始值不同。  
  
 删除报表模型时要特别小心。 如果删除模型，则将无法在报表生成器中打开和修改任何基于该模型的报表。 如果由于疏忽删除了现有报表使用的模型，则必须重新生成该模型、重新创建和保存使用该模型的任何报表，并重新指定要使用的任何模型项安全性。 不能仅重新生成模型然后将其附加到现有报表。  
  
## <a name="dependent-items"></a>依赖项  
 若要查看使用数据源的报表和模型的列表，请打开相应共享数据源的“依赖项”页。 在 Web 门户或 SharePoint 应用程序页中打开该数据源后即可访问此页。 请注意“依赖项”页不显示数据驱动订阅。 如果共享数据源是由订阅使用，则该订阅将不会显示在依赖项列表中。  
  
 **查看 SharePoint 中的依赖项**  
  
1.  打开包含 .rsds 文件的库。  
  
2.  指向共享数据源。  
  
3.  单击以显示向下箭头，然后选择 **“查看依赖项”** 。  
  
     对于报表模型，依赖项列表将显示在报表生成器中创建的报表。 对于共享数据源，依赖项列表可以包括报表和报表模型。  
  
## <a name="see-also"></a>另请参阅  
 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [管理报表数据源](../../reporting-services/report-data/manage-report-data-sources.md)   
 [配置分页报表的数据源属性](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
