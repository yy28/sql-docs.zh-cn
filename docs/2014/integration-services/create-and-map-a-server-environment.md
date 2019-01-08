---
title: 创建和映射服务器环境 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isenvprop.variables.f1
- sql12.ssis.ssms.iscreateenv.f1
- sql12.ssis.ssms.isenvprop.permissions.f1
- sql12.ssis.ssms.isenvprop.general.f1
ms.assetid: b1cbb697-713f-48e4-b234-b23724d87451
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1116cc2e1040326237a31039fa2b52618c3f559e
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52408224"
---
# <a name="create-and-map-a-server-environment"></a>创建和映射服务器环境
  创建服务器环境来指定已部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器的项目中所含包的运行时值。 您可以随后针对特定包、入口点包或给定项目中的所有包，将环境变量映射到参数。 入口点包通常是执行子包的父包。  
  
> [!IMPORTANT]  
>  对于给定的执行，只能使用单个服务器环境中包含的值来执行包。  
  
 您可以查询视图以获得服务器环境、环境引用和环境变量的列表。 您也可以调用存储过程来添加、删除和修改环境、环境引用和环境变量。 有关详细信息，请参阅 [SSIS Catalog](catalog/ssis-catalog.md) 中的“服务器环境、服务器变量和服务器环境引用”一节。  
  
### <a name="to-create-and-use-a-server-environment"></a>创建和使用服务器环境  
  
1.  在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中，在对象资源管理器中依次展开“[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目录”> **SSISDB** 节点，找到要为其创建环境的项目的“环境”文件夹。  
  
2.  右键单击“环境”文件夹，然后单击“创建环境”。  
  
3.  为环境键入名称和说明（可选），然后单击 **“确定”**。  
  
4.  右键单击该新环境，然后单击“属性”。  
  
5.  在 **“变量”** 页上，执行以下操作以便添加变量。  
  
    1.  选择变量的 **“类型”** 。 变量的名称 **无需** 匹配您将映射到该变量的项目参数的名称。  
  
    2.  输入变量的可选 **“说明”** 。  
  
    3.  输入环境变量的 **“值”** 。  
  
         有关环境变量名称的规则的信息，请参阅 [SSIS Catalog](catalog/ssis-catalog.md) 中的“环境变量”一节。  
  
    4.  通过选中或取消选中 **“敏感”** 复选框，指示该变量是否包含敏感值。  
  
         如果您选择 **“敏感”**，则变量值不会显示在 **“值”** 字段中。  
  
         敏感值在 SSISDB 目录中进行加密。 有关加密的详细信息，请参阅 [SSIS Catalog](catalog/ssis-catalog.md)。  
  
6.  在 **“权限”** 页上，通过执行以下操作，授予或拒绝所选用户和角色的权限。  
  
    1.  单击 **“浏览”**，然后在 **“浏览所有主体”** 对话框中选择一个或多个用户和角色。  
  
    2.  在 **“登录名或角色”** 区域中，选择您要为其授予或拒绝权限的用户或角色。  
  
    3.  在 **“显式”** 区域中，单击每个权限旁边的 **“授予”** 或 **“拒绝”** 。  
  
7.  若要编写环境的脚本，请单击 **“脚本”**。 默认情况下，该脚本显示在一个新的查询编辑器窗口中。  
  
    > [!TIP]  
    >  对环境属性进行了更改（例如添加变量）后，并且在“环境属性”对话框中单击“确定”前，需要单击“脚本”。 否则，将不会生成脚本。  
  
8.  单击 **“确定”** 保存对环境属性的更改。  
  
9. 在对象资源管理器的 **SSISDB** 节点下，展开“项目”文件夹，右键单击项目，然后单击“配置”。  
  
10. 在 **“引用”** 页上，单击 **“添加”** 以便添加一个环境，然后单击 **“确定”** 以便保存对该环境的引用。  
  
11. 再次右键单击该项目，然后单击“配置”。  
  
12. 若要将环境变量映射到在设计时添加到包的参数，或映射到将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目转换为项目部署模型时生成的参数，请执行以下操作。  
  
    1.  在 **“参数”** 页上的 **“参数”** 选项卡中，单击 **“值”** 字段旁边的浏览按钮。  
  
    2.  单击 **“使用环境变量”**，然后选择已创建的环境变量。  
  
13. 若要将环境变量映射到连接管理器属性，请执行以下操作。 将在 SSIS 服务器上为连接管理器属性自动生成参数。  
  
    1.  在 **“参数”** 页上的 **“连接管理器”** 选项卡中，单击 **“值”** 字段旁边的浏览按钮。  
  
    2.  单击 **“使用环境变量”**，然后选择已创建的环境变量。  
  
14. 单击 **“确定”** 两次以保存所做的更改。  
  
  
