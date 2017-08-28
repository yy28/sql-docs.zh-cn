---
title: "OData 连接管理器 |Microsoft 文档"
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
caps.latest.revision: 9
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: f54562b59e8c61f723c17e2812ca39cb2e95f273
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="odata-connection-manager"></a>OData 连接管理器
 连接到 OData 数据源与 OData 连接管理器。 OData 源组件使用 OData 连接管理器连接到 OData 数据源和使用从服务的数据。 有关详细信息，请参阅 [OData Source](../../integration-services/data-flow/odata-source.md)。  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>向 SSIS 包添加 OData 连接管理器  
 可以将新的 OData 连接管理器添加到 SSIS 包通过三种方式：  
  
-   单击 **“OData 源编辑器”** 中的 **“新建…”**  
  
-   在“解决方案资源管理器”  中，右键单击“连接管理器” 文件夹，然后单击“新建连接管理器” 。 为 **“连接管理器类型”** 选择 **“ODATA”**。  
  
-   在中右击**连接管理器**在包设计器中，，然后选择底部窗格中**新连接**。 为 **“连接管理器类型”** 选择 **“ODATA”**。  
  
## <a name="connection-manager-authentication"></a>连接管理器身份验证  
 OData 连接管理器支持身份验证的五种的模式。  
  
-   Windows 身份验证  
  
-   基本身份验证（使用用户名和密码）  

-   Microsoft Dynamics AX Online（使用用户名和密码）
  
-   Microsoft Dynamics CRM Online （使用用户名和密码）
  
-   Microsoft Online Services（使用用户名和密码）  
  
对于匿名访问，请选择“Windows 身份验证”选项。  

若要连接到 Microsoft Dynamics AX Online 或 Microsoft Dynamics CRM online，你不能使用**Microsoft Online Services**身份验证选项。 你还不能使用多因素身份验证配置任何选项。
  
### <a name="specifying-and-securing-credentials"></a>指定和保护凭据  
 如果 OData 服务需要基本身份验证，则可以在 [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)中指定用户名和密码。 在编辑器中输入的值保留在包中。 密码值根据包保护级别进行加密。  
  
 有几种方法来参数化用户名和密码值或将其存储在包外。 例如，你可以使用参数，或从 SQL Server Management Studio 运行包时直接设置连接管理器属性。  
  
## <a name="odata-connection-manager-properties"></a>OData 连接管理器属性  
 以下列表介绍 OData 连接管理器的属性。  
  
|||  
|-|-|  
|属性|Description|  
|Url|服务文档的 URL。|  
|UserName|要用于身份验证，如果所需的用户名。|  
|密码|要用于身份验证，如果所需的密码。|  
|SubQueries|包括连接管理器的其他属性。|  
  
## <a name="odata-connection-manager-editor"></a>“OData 连接管理器编辑器”
  使用**OData 连接管理器编辑器**对话框以添加连接或编辑现有连接到 OData 数据源。  
  
### <a name="options"></a>选项  
 **连接管理器名称**  
 连接管理器的名称。  
  
 **服务文档位置**  
 OData 服务的 URL。 例如：http://services.odata.org/V3/Northwind/Northwind.svc/。  
  
 **身份验证**  
选择以下选项之一：
-   **Windows 身份验证**。 对于匿名访问，请选择此选项。
-   **基本身份验证** 
-   **Microsoft Dynamics AX 联机**为 Dynamics AX 联机
-   **Microsoft Dynamics CRM Online**为 Dynamics CRM Online
-   **Microsoft Online Services** Microsoft Online services

如果你选择 Windows 身份验证之外的一个选项，输入**用户名**和**密码**。 

若要连接到 Microsoft Dynamics AX Online 或 Microsoft Dynamics CRM online，你不能使用**Microsoft Online Services**身份验证选项。 你还不能使用多因素身份验证配置任何选项。

 **测试连接**  
 单击此按钮可测试与 OData 源的连接。  

