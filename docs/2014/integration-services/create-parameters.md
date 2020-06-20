---
title: 创建参数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.parameterwindow.f1
ms.assetid: cd5d675b-dd5d-49cc-8b1f-dc717a973f99
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f43c6f25d7360b558a8bbfb9887b6bd2d6362106
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84917213"
---
# <a name="create-parameters"></a>Create Parameters
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 可以创建项目参数和包参数。 下面的过程提供了有关创建包参数/项目参数的分步说明。  
  
> [!NOTE]  
>  若要将使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的早期版本创建的项目转换为项目部署模型，则可以使用 **“Integration Services 项目转换向导”** 来创建基于配置的参数。 有关详细信息，请参阅 [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md)。  
  
### <a name="to-create-package-parameters"></a>创建包参数  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中打开包，然后在 SSIS 设计器中单击 **“参数”** 选项卡。  
  
     ![包参数选项卡](media/denali-package-parameters.gif "包参数选项卡")  
  
2.  单击工具栏上的 **“添加参数”** 按钮。  
  
     ![添加工具栏按钮](media/denali-parameter-add.gif "添加工具栏按钮")  
  
3.  为列表自身中或 **“属性”** 窗口中的 **“名称”**、 **“数据类型”**、 **“值”**、 **“敏感”** 和 **“必需”** 属性输入值。 下表对这些属性进行了说明：  
  
    |属性|说明|  
    |--------------|-----------------|  
    |名称|参数的名称。|  
    |数据类型|参数的数据类型。|  
    |默认值|在设计时分配的参数的默认值。 这也称为设计默认值。|  
    |敏感|敏感参数值在目录中加密，并且在使用 Transact-SQL 或 SQL Server Management Studio 查看时以 NULL 值的形式出现。|  
    |必需|需要首先指定并非设计默认值的值，包才能执行。|  
    |说明|出于可维护性目的而提供的参数的说明。 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，当在适用的参数窗口中选择参数时，在“Visual Studio 属性”窗口中设置参数说明。|  
  
    > [!NOTE]  
    >  在您向目录部署某一项目时，还有几个属性将与该项目相关联。 若要查看目录中所有参数的全部属性，请使用 [catalog.object_parameters（SSISDB 数据库）](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database)视图。  
  
4.  保存项目以保存对参数所做的更改。 参数值将存储在项目文件中。  
  
    > [!WARNING]  
    >  可以直接在列表中编辑，也可以使用“属性”窗口来修改参数属性的值。**** 可以使用“删除 (X)”工具栏按钮来删除参数。**** 使用最后一个工具栏按钮，可以为仅在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中执行包时使用的参数指定值。  
  
    > [!NOTE]  
    >  如果未在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中打开项目便重新打开包文件，则“参数”选项卡将为空且被禁用。****  
  
### <a name="to-create-project-parameters"></a>创建项目参数  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中打开项目。  
  
2.  在解决方案资源管理器中右键单击“Project.params”，然后单击“打开”，或者双击“Project.params”将其打开。************  
  
     ![项目参数窗口](media/denali-project-parameters.gif "项目参数窗口")  
  
3.  单击工具栏上的 **“添加参数”** 按钮。  
  
     ![添加工具栏按钮](media/denali-parameter-add.gif "添加工具栏按钮")  
  
4.  为 **“名称”**、 **“数据类型”**、 **“值”**、 **“敏感”** 和 **“必需”** 属性输入值。  
  
    |属性|说明|  
    |--------------|-----------------|  
    |名称|参数的名称。|  
    |数据类型|参数的数据类型。|  
    |默认值|在设计时分配的参数的默认值。 这也称为设计默认值。|  
    |敏感|敏感参数值在目录中加密，并且在使用 Transact-SQL 或 SQL Server Management Studio 查看时以 NULL 值的形式出现。|  
    |必需|需要首先指定并非设计默认值的值，包才能执行。|  
    |说明|出于可维护性目的而提供的参数的说明。 在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，当在适用的参数窗口中选择参数时，在“Visual Studio 属性”窗口中设置参数说明。|  
  
5.  保存项目以保存对参数所做的更改。 参数值将存储在项目文件的配置中。 保存项目文件以将对参数值的所有更改提交到磁盘。  
  
    > [!WARNING]  
    >  可以直接在列表中编辑，也可以使用“属性”窗口来修改参数属性的值。**** 可以使用“删除 (X)”工具栏按钮来删除参数。**** 使用最后一个工具栏按钮打开 **“管理参数值”** 对话框，您可以为仅在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中执行包时使用的参数指定值。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSIS&#41; 参数 Integration Services](integration-services-ssis-package-and-project-parameters.md)  
  
  
