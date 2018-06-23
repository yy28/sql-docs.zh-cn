---
title: 设置或更改包的保护级别 |Microsoft 文档
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services],security
- security [Integration Services],protection levels
- protection level for packages [Integration Services]
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 695667f3ba50b6cde3d2b9629e7116fecf7c4b16
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127745"
---
# <a name="set-or-change-the-protection-level-of-packages"></a>设置或更改包的保护级别
  若要控制对包内容以及其中包含的敏感值（如密码）的访问，请设置 `ProtectionLevel` 属性的值。 项目中所含的包需要具有与项目相同的保护级别才能生成项目。 如果更改项目的 `ProtectionLevel` 属性设置，需要为包手动更新该属性设置。  
  
 有关如何确定`ProtectionLevel`适用设置包的不同阶段在包生命周期，请参阅[Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md)。 有关 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中安全功能的概述，请参阅[安全性概述 (Integration Services)](security/security-overview-integration-services.md)。  
  
 本主题中的过程描述如何使用[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]或 dtutil 命令提示实用工具，来更改`ProtectionLevel`属性。  
  
> [!NOTE]  
>  除了本主题中的过程，通常可以设置或更改`ProtectionLevel`包时导入或导出包的属性。 当使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导保存包时，您也可以更改包的 `ProtectionLevel` 属性。  
  
### <a name="to-set-or-change-the-protection-level-of-a-package-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中设置或更改包的保护级别  
  
1.  查看的可用值`ProtectionLevel`在主题中，属性[设置包保护级别](security/access-control-for-sensitive-data-in-packages.md)，并确定你的程序包的相应值。  
  
2.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含该包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中打开包。  
  
4.  如果“属性”窗口未显示包的属性，请单击设计图面。  
  
5.  在属性窗口中，在**安全**组中，选择适当的值`ProtectionLevel`属性。  
  
     如果选择的保护级别需要密码，请输入密码作为 **PackagePassword** 属性的值。  
  
6.  在 **“文件”** 菜单上，选择 **“保存选定项”** 以保存修改的包。  
  
### <a name="to-set-or-change-the-protection-level-of-packages-at-the-command-prompt"></a>在命令提示符下设置或更改包的保护级别  
  
1.  查看的可用值`ProtectionLevel`在主题中，属性[设置包保护级别](security/access-control-for-sensitive-data-in-packages.md)，并确定你的程序包的相应值。  
  
2.  查看的映射`Encrypt`在主题中，选项[dtutil Utility](dtutil-utility.md)，并确定要用作所选的值的相应整数`ProtectionLevel`属性。  
  
3.  打开命令提示符窗口。  
  
4.  在命令提示符处，导航到包含或多个你想要设置的包的文件夹`ProtectionLevel`属性。  
  
     下面步骤中所示的语法示例假设此文件夹是当前文件夹。  
  
5.  使用与下列示例之一相类似的命令，设置或更改包的保护级别。  
  
    -   下面的命令集`ProtectionLevel`为级别 2，"使用密码加密敏感"，密码为"strongpassword"文件系统中的单个包的属性：  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   下面的命令将文件系统中特定文件夹内所有包的 `ProtectionLevel` 属性设置为级别 2“使用密码加密敏感数据”，密码为“strongpassword”：  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         如果您在批文件中使用类似的命令，则请输入文件占位符“%f”作为批文件中的“%%f”。  
  
## <a name="see-also"></a>请参阅  
 [dtutil 实用工具](dtutil-utility.md)  
  
  