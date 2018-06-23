---
title: 选择包管理选项 （SSIS 包升级向导） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.is.upgradewizard.selectpackagemgtoptions.f1
ms.assetid: 810fc020-51cd-43ed-9f35-af99b4f35947
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a1a05db41d0e82b931f51a7f3c0e80f8d33de79c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129039"
---
# <a name="select-package-management-options-ssis-package-upgrade-wizard"></a>选择包管理选项（SSIS 包升级向导）
  使用 **“选择包管理选项”** 页指定用于对包进行升级的选项。  
  
 **运行 SSIS 包升级向导**  
  
-   [使用 SSIS 包升级向导升级 Integration Services 包](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="options"></a>“常规”  
 **更新连接字符串以使用新的提供程序名称**  
 更新连接字符串以使用当前版本的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的下列提供程序的名称：  
  
-   用于 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的 OLE DB 提供程序  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包升级向导仅更新存储在连接管理器中的连接字符串。 向导不会更新通过使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 表达式语言或在脚本任务中使用代码动态构造的连接字符串。  
  
 **验证升级包**  
 验证升级包，并仅保存通过验证的升级包。  
  
 如果未选择此选项，则向导将不会验证升级包。 因此，向导将保存所有升级包，不论包是否有效。 向导会将升级包保存到在向导的“选择目标位置”页上指定的目标。  
  
 验证会延长升级过程的时间。 对于可能成功升级的大型包，建议不要选择此选项。  
  
 **创建新的包 ID**  
 为升级包创建新的包 ID。  
  
 **包升级失败时继续执行升级过程**  
 指定当无法升级某个包时 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包升级向导继续升级剩余包。  
  
 **包名称冲突**  
 指定向导应如何处理同名的包。 此选项具有下表所列的值。  
  
 **覆盖现有包文件**  
 使用同名的升级包替换现有包。  
  
 **添加数值后缀以升级包名称**  
 向升级包名称添加数值后缀。  
  
 **不要升级包**  
 停止升级包，并在完成向导时显示错误。  
  
 当在向导的 **“选择目标位置”** 页上选择 **“保存到源位置”** 选项时，上述选项不可用。  
  
 **忽略配置**  
 包在升级过程中未加载包配置。 选择此选项可缩短升级程序包所需的时间。  
  
 **备份原始包**  
 使向导将原始包备份到 **SSISBackupFolder** 文件夹。 向导会创建 **SSISBackupFolder** 文件夹，将其作为包含原始包和升级包的文件夹的子文件夹。  
  
> [!NOTE]  
>  仅当指定将原始包和升级的包都存储在文件系统中且在同一文件中时，此选项才可用。  
  
 有关详细信息，请参阅 [使用 SSIS 包升级向导升级 Integration Services 包](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)。  
  
## <a name="see-also"></a>请参阅  
 [升级 Integration Services 包](install-windows/upgrade-integration-services-packages.md)  
  
  