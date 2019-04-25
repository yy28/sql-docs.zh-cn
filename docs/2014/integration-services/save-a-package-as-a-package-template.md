---
title: 将包保存为包模板 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- reusing packages
- templates [Integration Services]
ms.assetid: efe66cec-3933-4f6e-8d35-fe3d300de66c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 79652d50bb4df2bf80ec9f072e8828db9935368f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766799"
---
# <a name="save-a-package-as-a-package-template"></a>将包另存为包模板
  本主题介绍在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中创建新的 Integration Services 包时如何指定自定义包以及将自定义包作为模板。 默认情况下，在将新包添加到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中时， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 使用创建空包的包模板。 您无法替换此默认模板，但可以添加新的模板。  
  
 可以指定多个包用作模板。 必须先创建这些包，然后才能实现将自定义包作为模板。  
  
 使用自定义包作为模板来创建包时，新的包将具有与模板相同的名称和 GUID。 若要区分这些包，应当更新 `Name` 属性的值，并为 `ID` 属性生成新的 GUID。 有关详细信息，请参阅 [在 SQL Server Data Tools 中创建包](create-packages-in-sql-server-data-tools.md) 和 [设置包属性](set-package-properties.md)。  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>将自定义包指定为包模板  
  
1.  在文件系统中，找到要用作模板的包。  
  
2.  将此包复制到 DataTransformationItems 文件夹中。 默认情况下，此文件夹位于 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject。  
  
3.  对每个要用作模板的包重复步骤 1 和 2。  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>使用自定义包作为包模板  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要在其中创建包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，右键单击项目，指向“添加”，然后单击“新建项”。  
  
3.  在“添加新项 —\<项目名称>”对话框中，单击要用作模板的包。  
  
     模板列表包括名为“新建 SSIS 包”的默认包模板。 包图标将标识可以用作包模板的模板。  
  
4.  单击 **“添加”**。  
  
## <a name="see-also"></a>请参阅  
 [在 SQL Server Data Tools 中创建包](create-packages-in-sql-server-data-tools.md)   
 [Integration Services (SSIS) 包](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
