---
title: 设置或更改包的保护级别 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services],security
- security [Integration Services],protection levels
- protection level for packages [Integration Services]
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
caps.latest.revision: 10
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 94d29f4e488e68c5fda2549b793a26770480e30a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201647"
---
# <a name="set-or-change-the-protection-level-of-packages"></a>设置或更改包的保护级别
  若要控制对包内容以及其中包含的敏感值（如密码）的访问，请设置 `ProtectionLevel` 属性的值。 项目中所含的包需要具有与项目相同的保护级别才能生成项目。 如果更改项目的 `ProtectionLevel` 属性设置，需要为包手动更新该属性设置。  
  
 有关如何确定`ProtectionLevel`设置适用于您的包的不同阶段中的包的生命周期，请参阅[包中敏感数据的访问控制](security/access-control-for-sensitive-data-in-packages.md)。 有关 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中安全功能的概述，请参阅[安全性概述 (Integration Services)](security/security-overview-integration-services.md)。  
  
 本主题中的过程描述如何使用两种[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]或 dtutil 命令提示实用工具来更改`ProtectionLevel`属性。  
  
> [!NOTE]  
>  除了本主题中的过程，您通常可以设置或更改`ProtectionLevel`包时导入或导出包的属性。 当使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导保存包时，您也可以更改包的 `ProtectionLevel` 属性。  
  
### <a name="to-set-or-change-the-protection-level-of-a-package-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中设置或更改包的保护级别  
  
1.  查看可用值`ProtectionLevel`主题中的属性[设置包的保护级别](security/access-control-for-sensitive-data-in-packages.md)，并确定您的包的对应值。  
  
2.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含该包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中打开包。  
  
4.  如果“属性”窗口未显示包的属性，请单击设计图面。  
  
5.  在属性窗口中**安全**组中，选择适当的值`ProtectionLevel`属性。  
  
     如果选择的保护级别需要密码，请输入密码作为 **PackagePassword** 属性的值。  
  
6.  在 **“文件”** 菜单上，选择 **“保存选定项”** 以保存修改的包。  
  
### <a name="to-set-or-change-the-protection-level-of-packages-at-the-command-prompt"></a>在命令提示符下设置或更改包的保护级别  
  
1.  查看可用值`ProtectionLevel`主题中的属性[设置包的保护级别](security/access-control-for-sensitive-data-in-packages.md)，并确定您的包的对应值。  
  
2.  查看有关映射`Encrypt`主题中的选项[dtutil 实用工具](dtutil-utility.md)，并确定要用作值的所选的相应整数`ProtectionLevel`属性。  
  
3.  打开命令提示符窗口。  
  
4.  在命令提示符处，导航到包含你想要设置的包的文件夹`ProtectionLevel`属性。  
  
     下面步骤中所示的语法示例假设此文件夹是当前文件夹。  
  
5.  使用与下列示例之一相类似的命令，设置或更改包的保护级别。  
  
    -   下面的命令集`ProtectionLevel`为级别 2"使用密码加密敏感"，密码为"strongpassword"文件系统中的单个包属性：  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   下面的命令将文件系统中特定文件夹内所有包的 `ProtectionLevel` 属性设置为级别 2“使用密码加密敏感数据”，密码为“strongpassword”：  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         如果您在批文件中使用类似的命令，则请输入文件占位符“%f”作为批文件中的“%%f”。  
  
## <a name="see-also"></a>请参阅  
 [dtutil 实用工具](dtutil-utility.md)  
  
  
