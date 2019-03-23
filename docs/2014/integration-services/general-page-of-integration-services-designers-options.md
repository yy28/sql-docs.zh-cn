---
title: 常规页 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Business_Intelligence_Designers.Data_Transformation_Designers.General
ms.assetid: d695690a-923b-4036-945e-7621e8651deb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f27ec0c9fe8078bb11a48114a3d456793271853d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391755"
---
# <a name="general-page"></a>“常规”页
  使用 **“选项”** 对话框中 **“Integration Services 设计器”** 页的 **“常规”** 页，可以指定用于加载、显示和升级包的选项。  
  
 若要打开 **“常规”** 页，请在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，单击 **“工具”** 菜单上的 **“选项”**，展开 **“商业智能设计器”**，然后选择 **“Integration Services 设计器”**。  
  
## <a name="options"></a>选项  
 **加载包时检查数字签名**  
 选择让 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 在加载包时检查数字签名。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 仅会检查数字签名是否存在、是否有效，并且是否来自可靠来源。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 不会检查包经过签名后是否发生过更改。  
  
 如果你设置 **BlockedSignatureStates** 注册表值，则此注册表值会替代“加载包时检查数字签名”  选项。 有关详细信息，请参阅[通过设置注册表值实现签名策略](implement-a-signing-policy-by-setting-a-registry-value.md)。  
  
 有关数字证书和包的详细信息，请参阅 [使用数字签名标识包的源](security/identify-the-source-of-packages-with-digital-signatures.md)。  
  
 **如果包未经签名则显示警告**  
 选择此项将在加载未经签名的包时显示警告。  
  
 **显示优先约束标签**  
 选择在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中查看包时，显示哪种优先约束标签（“成功”、“失败”或“完成”）。  
  
 **脚本语言**  
 选择新脚本任务和脚本组件的默认脚本语言。  
  
 **更新连接字符串以使用新的提供程序名称**  
 对于当前版本的 [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] ，打开或升级 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]包时，请将连接字符串更新为使用下列提供程序的名称：  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] OLE DB 访问接口  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包升级向导仅更新存储在连接管理器中的连接字符串。 向导不会更新通过使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 表达式语言或在脚本任务中使用代码动态构造的连接字符串。  
  
 **创建新的包 ID**  
 升级 [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] 包时，为包的升级版本创建新的包 ID。  
  
## <a name="see-also"></a>请参阅  
 [安全性概述 (Integration Services)](security/security-overview-integration-services.md)   
 [用脚本扩展包](extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
