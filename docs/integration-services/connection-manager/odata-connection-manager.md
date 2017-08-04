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
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 22374d52835c37ecf45fef20e15d563dad8e5917
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="odata-connection-manager"></a>OData 连接管理器
  使用 OData 连接管理器连接到 OData 源。 OData 源组件使用 OData 连接管理器连接到 OData 源并使用来自服务的数据。 有关详细信息，请参阅 [OData Source](../../integration-services/data-flow/odata-source.md)。  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>向 SSIS 包添加 OData 连接管理器  
 可以通过三种方式向 SSIS 包添加新 OData 连接管理器：  
  
-   单击 **“OData 源编辑器”** 中的 **“新建…”**  
  
-   在“解决方案资源管理器”  中，右键单击“连接管理器” 文件夹，然后单击“新建连接管理器” 。 为 **“连接管理器类型”** 选择 **“ODATA”**。  
  
-   右键单击包设计器底部的“连接管理器”  窗格，然后选择“新建连接…” 。 为 **“连接管理器类型”** 选择 **“ODATA”**。  
  
## <a name="connection-manager-authentication"></a>连接管理器身份验证  
 OData 连接管理器支持 5 种身份验证模式。  
  
-   Windows 身份验证  
  
-   基本身份验证（使用用户名和密码）  

-   Microsoft Dynamics AX Online（使用用户名和密码）
  
-   Microsoft Dynamics CRM Online （使用用户名和密码）
  
-   Microsoft Online Services（使用用户名和密码）  
  
 对于匿名访问，请选择“Windows 身份验证”选项。  
  
### <a name="specifying-and-securing-credentials"></a>指定和保护凭据  
 如果 OData 服务需要基本身份验证，则可以在 [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)中指定用户名和密码。 在编辑器中输入的值保留在包中。 密码值根据包保护级别进行加密。  
  
 有几种方法来参数化用户名和密码值或将其存储在包外。 例如，可以使用参数或在使用 SQL Server Management Studio 运行包时通过直接设置连接管理器属性来执行此操作。  
  
## <a name="odata-connection-manager-properties"></a>OData 连接管理器属性  
 下面的列表介绍 OData 连接管理器的属性。  
  
|||  
|-|-|  
|属性|Description|  
|Url|服务文档的 URL。|  
|UserName|要用于基本身份验证的用户名。|  
|密码|要用于基本身份验证的密码。|  
|ConnectionString|反映连接管理器的其他属性。|  
  
## <a name="see-also"></a>另请参阅  
 [OData 连接管理器编辑器](../../integration-services/connection-manager/odata-connection-manager-editor.md)  
  
  
