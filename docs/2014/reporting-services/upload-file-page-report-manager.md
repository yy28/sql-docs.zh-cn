---
title: 上载文件页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7bb3166f-9374-4449-b66a-ffb77298507d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1100baa3cd72a04d208b2076d91ca4efed7d38e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098869"
---
# <a name="upload-file-page-report-manager"></a>“上载文件”页（报表管理器）
  使用“上载文件”页可以将文件从文件系统发布到报表服务器数据库。 上载的文件将显示为报表服务器文件夹层次结构中的项。  
  
-   上载的 .rdl 文件将以报表形式发布到报表服务器。  
  
-   如果上载的 .smdl 文件包含数据源视图信息，则这些文件将作为报表模型发布。 如果这些文件缺少数据源视图引用，则上载时将出现错误。 如果从 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 报表模型项目上载 .smdl 文件，则数据源视图信息可能会丢失。 在报表模型项目中，数据源视图信息存储在 .smdl 文件之外的单独文件中。  
  
     包含数据源视图信息（因此能够成功上载）的模型文件是以前已发布到报表服务器、之后又从该服务器保存到文件系统上某文件的那些文件。 如果打开某模型的“常规属性”页，再单击 **“编辑”** 来打开该模型，则可以将该模型保存到文件，再将该文件作为新模型上载到报表服务器。 随后上载的 .smdl 文件将包含发布模型所需的所有信息。  
  
-   您上载的所有其他文件类型都将作为资源存储。 其中包括含有报表数据源连接信息的 .rds 文件。 上载 .rds 文件不会在报表服务器上生成共享数据源项。  
  
 所上载的项放在当前的文件夹中。 完成上载后，可以将该项移动至其他位置。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关的各版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅[SQL Server 2014 各个版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
### <a name="to-open-the-upload-file-page"></a>打开“上载文件”页  
  
1.  打开报表管理器，导航到要在其中上载文件的文件夹。  
  
2.  在工具栏上单击 **“上载文件”**。  
  
## <a name="options"></a>选项  
 **上载的文件**  
 显示要从文件系统复制的文件的全限定路径。  
  
 **“浏览”**  
 单击此选项可从文件系统中选择文件。  
  
 **名称**  
 键入文件的名称，文件名应与将在报表服务器命名空间中显示的名称一样。 名称必须至少包含一个字母数字字符。 还可以包含空格和某些符号。 在指定名称时，不得使用字符 ; ? : \@ & = +，$ * \< > |"或 / 时指定项名称。  
  
 **如果它存在，则覆盖该项**  
 如果希望将现有项替换为更新的版本，请选中此复选框。 若要覆盖现有版本，新项和现有项的名称必须完全相同。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [“内容”页（报表管理器）](../../2014/reporting-services/contents-page-report-manager.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [将文件上载到文件夹](report-server/upload-files-to-a-folder.md)  
  
  
