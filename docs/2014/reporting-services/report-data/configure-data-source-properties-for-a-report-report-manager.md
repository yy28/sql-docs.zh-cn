---
title: 配置报表的数据源属性（报表管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
ms.assetid: 27af5195-c845-40e0-9a9c-efe569424022
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7823ce29facb7f1c85a51a12b31ee2076a0d023b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107414"
---
# <a name="configure-data-source-properties-for-a-report--report-manager"></a>配置报表的数据源属性（报表管理器）
  在运行报表时，报表服务器检索属性信息以确定如何连接到数据源。 数据源类型、连接字符串和凭据信息在已发布报表的“数据源”属性页中指定。 可以设置这些属性以使数据源连接信息与创建报表时指定的原始值不同。  
  
 另外，如果具有已指定了要使用的连接信息的预定义共享数据源，则可以改为指定共享数据源。 若要使用共享数据源，请单击报表的“数据源属性”页上的 **“共享数据源”** 。  
  
### <a name="to-configure-an-embedded-data-source"></a>配置嵌入数据源  
  
1.  启动 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
2.  在报表管理器中，导航到 "**内容**" 页。 导航到要配置报表特定数据源的报表，然后打开该报表。  
  
3.  单击 "**属性**" 选项卡。此时将打开 "**常规**属性" 页。  
  
4.  单击 "**数据源**" 选项卡。这会打开报表的 "数据源属性" 页。  
  
5.  单击 **“自定义数据源”** 以指定报表内的数据源连接信息。  
  
6.  在 **“连接类型”** 列表中，指定用于处理来自数据源的数据的数据处理扩展插件。  
  
7.  对于 "**连接字符串**"，指定 Report Server 用于连接到数据源的连接字符串。 建议您不要在连接字符串中指定凭据。  
  
     下面的示例演示用于连接到本地[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]数据库的连接字符串：  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  对于 **“连接方式”**，请指定在报表运行时获取凭据的方式：  
  
    -   如果希望提示用户输入登录名和密码，请单击 **“运行该报表的用户提供的凭据”**。  
  
    -   如果希望将数据源与支持订阅或其他计划操作（如自动生成报表历史记录）的报表一起使用，请单击“安全存储在报表服务器中的凭据”****。  
  
    -   如果希望报表服务器将访问报表的用户的凭据传递给承载外部数据源的服务器，请单击 **“Windows 集成安全性”**。 在这种情况下，系统不会提示用户键入用户名或密码。  
  
    -   如果数据源不使用凭据（例如，如果数据源是通过文件系统访问的 XML 文件），请单击“不需要凭据”****。 仅当此凭据类型对于相应数据源有效时，才能指定它。 如果为要求身份验证的数据源选择此选项，则连接将失败。 如果选择此选项，请确保配置无人参与的执行帐户，以便在用户凭据不可用时，报表服务器可连接到其他计算机以检索数据或文件。  
  
 有关配置凭据的详细信息，请参阅 [指定报表数据源的凭据和连接信息](specify-credential-and-connection-information-for-report-data-sources.md)。 有关无人参与的执行帐户的详细信息，请参阅[配置无人参与的执行帐户（SSRS 配置管理器）](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
## <a name="see-also"></a>另请参阅  
 ["内容" 页 &#40;报表管理器&#41;](../contents-page-report-manager.md)   
 [新数据源页 &#40;报表管理器&#41;](../new-data-source-page-report-manager.md)   
 [创建、修改和删除共享数据源 &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)   
 [管理报表数据源](manage-report-data-sources.md)   
 [创建、删除或修改共享数据源 &#40;报表管理器&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [“数据源”属性页（报表管理器）](../data-sources-properties-page-report-manager.md)  
  
  
