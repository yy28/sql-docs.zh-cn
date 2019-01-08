---
title: 在 SQL Server Data Tools 中创建包 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: bb3c085b-1458-49fa-8348-6a76b6e97ea6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c2748cf548a6a5c60ceab764afb27fff111f3ea1
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372359"
---
# <a name="create-packages-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中创建包
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 设计器在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 中创建的包被保存到文件系统。 若要将包保存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或保存到包存储区，则需要保存包的副本。 有关详细信息，请参阅[保存一个包副本](../../2014/integration-services/save-a-copy-of-a-package.md)。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，可以使用以下方法之一来创建新包：  
  
-   使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含的包模板。  
  
-   使用自定义模板  
  
     若要使用自定义包作为创建新包的模板，只需将它们复制到 DataTransformationItems 文件夹中即可。 默认情况下，此文件夹位于 C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject。  
  
-   复制现有包。  
  
     如果现有包中包括了您希望重用的功能，则可以通过复制并粘贴其他包中的对象，在新包中更快地生成控制流和数据流。 有关在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中使用复制和粘贴的详细信息，请参阅 [重用包对象](reuse-of-package-objects.md)。  
  
     如果通过复制现有包或使用自定义包作为模板来创建新包，则现有包的名称和 GUID 也会被复制。 应当更新新包的名称和 GUID，以便将它与原始包区分开来。 例如，如果包有相同的 GUID，则难以识别日志数据属于哪个包。 您可以通过使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的“属性”窗口，重新生成 `ID` 属性中的 GUID 以及更新 `Name` 属性的值。 有关详细信息，请参阅 [设置包属性](set-package-properties.md) 和 [dtutil 实用工具](dtutil-utility.md)。  
  
-   使用已指定为模板的自定义包。  
  
-   运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导创建一个用于简单导入或导出的完整包。 此向导可以配置连接、源和目标，以及添加允许您立即运行导入或导出所需的任何数据转换。 您还可以保存包以便以后再次运行该包，或者在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中完善和增强该包。 但是，如果保存该包，则必须先将该包添加到现有的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中，然后才能更改该包或者在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中运行该包。  
  
 下列过程说明如何在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中创建或删除包。  
  
 有关演示如何使用默认的包模板创建基本包的视频，请参阅[创建基本包（SQL Server 视频）](https://go.microsoft.com/fwlink/?LinkId=131023)。  
  
### <a name="to-create-a-package-in-sql-server-data-tools-using-the-package-template"></a>在 SQL Server Data Tools 中使用报模板创建包  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要在其中创建包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，右键单击“SSIS 包”文件夹，然后单击“新建 SSIS 包”。  
  
3.  还可以向包中添加控制流、数据流任务和事件处理程序。 有关详细信息，请参阅[控制流](control-flow/control-flow.md)、[数据流](data-flow/data-flow.md)和[Integration Services (SSIS) 事件处理程序](integration-services-ssis-event-handlers.md)。  
  
4.  在 **“文件”** 菜单上，单击 **“保存选定项”** ，以保存新建的包。  
  
    > [!NOTE]  
    >  可以保存空包。  
  
  
