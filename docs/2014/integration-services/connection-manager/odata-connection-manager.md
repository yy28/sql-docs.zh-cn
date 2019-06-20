---
title: OData 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0b0596e9ba13e617b6f4eef961966bcc07107314
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833105"
---
# <a name="odata-connection-manager"></a>OData 连接管理器
  OData 连接管理器允许包连接到 OData 源。 OData 源组件使用 OData 连接管理器连接到 OData 源并使用来自服务的数据。 请参阅[OData 源](../data-flow/odata-source.md)部分，了解详细信息，包括这些组件的安装说明。  
  
## <a name="adding-connection-manager-to-an-ssis-package"></a>向 SSIS 包添加连接管理器  
 可以通过三种方式向 SSIS 包添加新 OData 连接管理器：  
  
-   单击“OData 源编辑器”中的“新建…”按钮  
  
-   右键单击**连接管理器**中的文件夹**解决方案资源管理器**然后单击**新连接管理器**。 为 **“连接管理器类型”** 选择 **“ODATA”**。  
  
-   在中右击**连接管理器**包设计器中，然后选择底部窗格**新建连接...**.为 **“连接管理器类型”** 选择 **“ODATA”**。  
  
## <a name="connection-manager-authentication"></a>连接管理器身份验证  
 OData 连接管理器支持两种身份验证模式。  
  
-   Windows 身份验证  
  
-   基本身份验证（用户名/密码）  
  
 对于匿名访问，请选择“Windows 身份验证”选项  
  
### <a name="specifying-and-securing-credentials"></a>指定和保护凭据  
 如果 OData 服务需要基本身份验证，则可以指定用户名和密码[OData 连接管理器编辑器](../odata-connection-manager-editor.md)。 在编辑器中输入的值保留在包中。 密码值根据包保护级别进行加密。  
  
 可通过多种方式外部化/参数化用户名和密码值。 要在 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)] 中实现此目的，有两种主要方式，使用参数或在使用 SQL Server Management Studio 运行包时直接设置连接管理器属性。  
  
## <a name="odata-connection-manager-properties"></a>OData 连接管理器属性  
 下面的列表介绍您可能需要更改的部分 OData 连接管理器属性。  
  
|||  
|-|-|  
|属性|Description|  
|Url|服务文档的 URL。|  
|UserName|要用于基本身份验证的用户名。|  
|Password|要用于基本身份验证的密码。|  
|ConnectionString|反映连接管理器的其他属性。|  
  
## <a name="see-also"></a>请参阅  
 [OData 连接管理器编辑器](../odata-connection-manager-editor.md)  
  
  
