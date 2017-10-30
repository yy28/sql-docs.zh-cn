---
title: "创建并部署为查找转换缓存 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- creating cache files for Lookup transformation
- deploying cache files for Lookup transformation
- Lookup transformation cache files
ms.assetid: cedf5cad-2fac-42d0-ad91-9461e117d330
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 88d6515c29c789c12818dfc51c86c5b1d4537247
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="create-and-deploy-a-cache-for-the-lookup-transformation"></a>为查找转换创建和部署缓存
  可以为查找转换创建和部署缓存文件 (.caw)。 引用数据集存储在缓存文件中。  
  
 查找转换通过将所连接数据源输入列中的数据和引用数据集中的列进行联接来执行查找。  
  
 可以使用缓存连接管理器和“缓存转换”转换来创建缓存文件。 有关详细信息，请参阅 [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md) 和 [Cache Transform](../../../integration-services/data-flow/transformations/cache-transform.md)。  
  
 若要了解查找转换和缓存文件的更多信息，请参阅 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)。  
  
### <a name="to-create-a-cache-file"></a>创建缓存文件  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 项目，再打开该包。  
  
2.  在 **“控制流”** 选项卡上，添加数据流任务。  
  
3.  在 **“数据流”** 选项卡上，向数据流添加“缓存转换”转换，再将该转换连接到数据源。  
  
     根据需要配置数据源。  
  
4.  双击缓存转换，在“缓存转换编辑器”中的“连接管理器”页上单击“新建”，创建一个新的缓存连接管理器。  
  
5.  在 **“缓存连接管理器编辑器”**的 **“常规”** 选项卡上，选择以下选项对缓存连接管理器进行配置，以保存缓存：  
  
    1.  选择 **“使用文件缓存”**。  
  
    2.  在 **“文件名”**中，键入文件路径。  
  
     运行包时，系统会创建该文件。  
  
    > [!NOTE]  
    >  包的保护级别不适用于缓存文件。 如果缓存文件包含敏感信息，可使用访问控制列表 (ACL) 来限制对存储该文件的位置或文件夹的访问。 应只允许访问某些帐户。 有关详细信息，请参阅 [访问包使用的文件](../../../integration-services/security/security-overview-integration-services.md#files)。  
  
6.  单击 **“列”** 选项卡，然后使用 **“索引位置”** 选项来指定哪些列是索引列。  
  
     对于非索引列，索引位置是 0。 对于索引列，索引位置是连续的正数。  
  
    > [!NOTE]  
    >  当将查找转换配置为使用缓存连接管理器时，则仅引用数据集中的索引列能够映射到输入列。 此外，还必须对所有索引列进行映射。  
  
     有关详细信息，请参阅 [Cache Connection Manager Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md)。  
  
7.  根据需要配置缓存转换。  
  
     有关详细信息，请参阅[缓存转换编辑器（“连接管理器”页）](../../../integration-services/data-flow/transformations/cache-transformation-editor-connection-manager-page.md)和[缓存转换编辑器（“映射”页）](../../../integration-services/data-flow/transformations/cache-transformation-editor-mappings-page.md)。  
  
8.  运行包。  
  
### <a name="to-deploy-a-cache-file"></a>部署缓存文件  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 项目，再打开该包。  
  
2.  创建包配置（可选）。 有关详细信息，请参阅 [创建包配置](../../../integration-services/packages/create-package-configurations.md)。  
  
3.  执行以下操作将缓存文件添加到项目：  
  
    1.  在解决方案资源管理器中，选择在步骤 1 中打开的项目。  
  
    2.  在“项目”菜单上，单击“添加现有项”。  
  
    3.  选择缓存文件，再单击 **“添加”**。  
  
     该文件将显示在解决方案资源管理器中的 **“杂项”** 文件夹。  
  
4.  配置项目以创建一个部署实用工具，再生成项目。 有关详细信息，请参阅 [Create a Deployment Utility](../../../integration-services/packages/create-a-deployment-utility.md)。  
  
     清单文件， \<*项目名称*>。SSISDeploymentManifest.xml，将创建一个列出的杂项文件项目、 包和包配置中。  
  
5.  将包部署到文件系统。 有关详细信息，请参阅 [Deploy Packages by Using the Deployment Utility](../../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建部署实用工具](../../../integration-services/packages/create-a-deployment-utility.md)  
  
  

