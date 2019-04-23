---
title: “转换 CRI”对话框（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10008"
helpviewer_keywords:
- CRI
- custom report items
ms.assetid: 2a3f2ac6-667e-4498-8b73-9c40beb993f5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1885d796d567d03585ae1ce0b591fb85bbf42658
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946810"
---
# <a name="convert-cri-dialog-box-report-builder"></a>“转换 CRI”对话框（报表生成器）
  该报表包含其中有不受支持的功能的自定义报表项 (CRI)。 CRI 是对报表定义语言 (RDL) 的扩展，它支持用于显示报表中的数据的自定义对象。 CRI 包含由第三方软件供应商提供的设计时和运行时组件。  
  
> [!NOTE]  
>  对于是否选择在报表服务器上支持自定义报表项，需要由系统管理员决定。 若要查看报表中的 CRI，必须将 CRI 组件安装在报表创作客户端上以预览报表，并将其安装在报表服务器上以查看已发布或上载的报表。 有关详细信息，请参阅 [Custom Report Items](../custom-report-items/custom-report-items.md)和第三方软件供应商提供的文档。  
  
 某些 CRI 可以转换为采用新的报表定义格式的报表项。 打开报表时，系统会提示您是否升级报表。 使用以下信息可以决定是否转换该报表中的 CRI：  
  
-   **是** 选择 **“是”** 将转换报表中所有可以转换的 CRI。 无法升级 CRI 中不受支持的功能，也不能从报表定义文件中删除它们。 有关不支持的功能的列表，请参阅 [升级报表](../install-windows/upgrade-reports.md)。 查看报表时，可能看到 CRI 在报表中的显示方式存在差异。  
  
-   **否** ：如果不希望转换报表中的 CRI，请选择 **“否”** 。 当前版本中的报表处理器无法显示这些 CRI。 如果您的系统管理员计划安装从第三方软件供应商那里得到的且与新报表定义格式兼容的新版本 CRI，则应当选择 **“否”**。 在使用新版本以前，CRI 将作为带有红色 X 的空文本框显示在报表中。  
  
 在上述两种情况下，报表都将升级到新的报表定义格式，并将原始报表的备份副本另存为 \<Report Name> `-` Backup.rdl。 如果在报表创作工具中保存报表，则会以新的报表定义格式保存升级的报表。 如果发布报表，则报表首先保存在您的计算机上，然后发布到报表服务器。 您需要将报表的升级版本发布到报表服务器。  
  
 如果不保存报表，则原始报表将保持不变。 但是，不能在比 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 更高的版本中或在使用此报表定义格式的报表创作环境中编辑该报表。 对于报表的原始版本，通过使用报表管理器将它上载到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器，可以继续运行它。 有关详细信息，请参阅[上传文件或报表（报表管理器）](../reports/upload-a-file-or-report-report-manager.md)。  
  
 对于上载而不是发布到报表服务器的报表，报表处理器将在第一次使用该报表时确定是否可以将它升级。 对于无法升级的报表，将以向后兼容模式对其进行处理，并像在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的早期版本中那样继续显示它们。 有关更多信息，请参见 [Upgrade Reports](../install-windows/upgrade-reports.md)。  
  
 若要标识报表、报表服务器或报表创作环境的当前报表定义格式，请参阅[查找报表定义架构版本 (SSRS)](../reports/find-the-report-definition-schema-version-ssrs.md)。  
  
## <a name="see-also"></a>请参阅  
 [用于对话框、窗格和向导的报表生成器帮助](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
