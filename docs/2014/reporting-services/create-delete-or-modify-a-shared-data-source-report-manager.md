---
title: 创建、 删除或修改共享的数据源 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- removing shared data sources
- data sources [Reporting Services], shared
- deleting shared data sources
- modifying shared data sources
ms.assetid: cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 99e083439e49d522ddc84f1f32454b0c4777237b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025868"
---
# <a name="create-delete-or-modify-a-shared-data-source-report-manager"></a>创建、删除或修改共享数据源（报表管理器）
  共享数据源指定数据源的连接属性。 如果数据源供大量的报表、模型或数据驱动订阅使用，则可考虑创建共享数据源，以消除必须在多个位置维护相同连接信息的开销。  
  
 下面的图标表示报表管理器文件夹层次结构中的共享数据源：  
  
 ![共享数据源图标](media/hlp-16datasource.png "共享数据源图标")  
共享数据源图标  
  
### <a name="to-create-a-shared-data-source"></a>创建共享数据源  
  
1.  启动 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)。  
  
2.  在报表管理器中，导航到 **“内容”** 页。  
  
3.  单击 **“新建数据源”**。 此时，将打开 **“新建数据源”** 页。  
  
4.  为相应项键入一个名称。 名称必须包含至少一个字符并且必须以字母开头。 它也可以包括特定的一些符号，但不能包括空格或以下字符：; ? : \@ & = + , $ / * \< > | " /.  
  
5.  根据需要，可以键入说明，向用户提供相关的连接信息。 此说明将显示在报表管理器的 **“内容”** 页中。  
  
6.  在 **“数据源类型”** 列表中，指定用于处理来自数据源的数据的数据处理扩展插件。  
  
7.  对于 **“连接字符串”**，指定报表服务器用于连接数据源的连接字符串。 建议您不要在连接字符串中指定凭据。  
  
     下面的示例演示用于连接到本地 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库的连接字符串：  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  对于 **“连接方式”**，请指定在报表运行时获取凭据的方式：  
  
    -   如果希望提示用户输入登录名和密码，请单击 **“运行该报表的用户提供的凭据”**。 若要将用户输入的凭据作为 Windows 凭据，请单击 **“在与数据源建立连接时用作 Windows 凭据”**。 如果用户名和密码是数据库凭据，则不选择此选项。  
  
    -   如果要将该数据源用作共享数据源以及使用由数据源所有者管理的已保存凭据，或者将该数据源用于支持订阅或其他计划操作（例如自动生成报表历史记录）的报表，请单击“安全存储在报表服务器中的凭据”。 如果数据库服务器支持模拟或委托，则可以选择 **“与数据源建立连接之后模拟经过身份验证的用户”**。  
  
    -   如果希望报表服务器将访问报表的用户的凭据传递给承载外部数据源的服务器，请单击 **“Windows 集成安全性”**。 在这种情况下，系统不会提示用户键入用户名或密码。  
  
    -   如果数据源不使用凭据（例如，如果数据源是通过文件系统访问的 XML 文件），请单击“不需要凭据”。 仅当此凭据类型对于相应数据源有效时，才能指定它。 如果为要求身份验证的数据源选择此选项，则连接将失败。 如果选择此选项，请确保配置无人参与的执行帐户，以便在用户凭据不可用时，报表服务器可连接到其他计算机以检索数据或文件。  
  
     有关配置凭据的详细信息，请参阅 [指定报表数据源的凭据和连接信息](report-data/specify-credential-and-connection-information-for-report-data-sources.md)。 有关无人参与的执行帐户的详细信息，请参阅[配置无人参与的执行帐户（SSRS 配置管理器）](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
9. 单击 **“测试连接”** 按钮可验证数据源配置。  
  
    > [!NOTE]  
    >  对于 XML 数据源类型，不支持“测试连接”按钮。  
  
10. 单击 **“确定”**。  
  
### <a name="to-modify-a-shared-data-source"></a>修改共享数据源  
  
1.  在报表管理器中，导航到“内容”页。  
  
2.  导航到共享数据源项，悬停在该项上，单击下拉列表，然后从上下文菜单中单击“管理”。 **“属性”** 页将打开。  
  
3.  修改数据源，再单击 **“应用”**。  
  
### <a name="to-delete-a-shared-data-source"></a>删除共享数据源  
  
-   在报表管理器中，导航到 **“内容”** 页，再执行以下操作之一：  
  
    -   导航到共享数据源项。  
  
         单击该项将其打开。 此时将打开“常规属性”页。  
  
         单击 **“删除”**，再单击 **“确定”**。  
  
    -   在 **“内容”** 页中，导航到要删除的数据源所在的文件夹。  
  
         悬停在该项上，单击下拉列表，然后从上下文菜单中单击“删除”。  
  
         [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [数据连接、 数据源和 Reporting Services 中的连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [“内容”页（报表管理器）](../../2014/reporting-services/contents-page-report-manager.md)   
 [创建、修改和删除共享数据源 (SSRS)](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [管理报表数据源](report-data/manage-report-data-sources.md)   
 [配置报表的数据源属性（报表管理器）](report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
