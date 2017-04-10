---
title: "设置或更改包的保护级别 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "密码 [Integration Services]"
  - "包 [Integration Services], 安全性"
  - "安全性 [Integration Services], 保护级别"
  - "包的保护级别 [Integration Services]"
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# 设置或更改包的保护级别
  若要控制对包内容以及其中包含的敏感值（如密码）的访问，请设置 **ProtectionLevel** 属性的值。 项目中所含的包需要具有与项目相同的保护级别才能生成项目。 如果更改项目的 **ProtectionLevel** 属性设置，需要为包手动更新该属性设置。  
  
 有关如何确定包在包生命周期中的不同阶段所对应的 **ProtectionLevel** 设置的信息，请参阅 [Access Control for Sensitive Data in Packages](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)。 有关 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中安全功能的概述，请参阅[安全性概述 (Integration Services)](../../integration-services/security/security-overview-integration-services.md)。  
  
 本主题中的过程介绍如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 dtutil 命令提示实用工具来更改 **ProtectionLevel** 属性的值。  
  
> [!NOTE]  
>  除了本主题中的过程外，当导入或导出包时，您通常可以设置或更改包的 **ProtectionLevel** 属性。 当使用 **ProtectionLevel** 导入和导出向导保存包时，您也可以更改包的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 属性。  
  
### 在 SQL Server Data Tools 中设置或更改包的保护级别  
  
1.  在主题 **设置包的保护级别** 中查看 [ProtectionLevel](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)属性的可用值，然后确定您的包的对应值。  
  
2.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含该包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中打开包。  
  
4.  如果“属性”窗口未显示包的属性，请单击设计图面。  
  
5.  在“属性”窗口中的 **“安全性”** 组，为 **ProtectionLevel** 属性选择相应的值。  
  
     如果选择的保护级别需要密码，请输入密码作为 **PackagePassword** 属性的值。  
  
6.  在 **“文件”** 菜单上，选择 **“保存选定项”** 以保存修改的包。  
  
### 在命令提示符下设置或更改包的保护级别  
  
1.  在主题 **设置包的保护级别** 中查看 [ProtectionLevel](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)属性的可用值，然后确定您的包的对应值。  
  
2.  在主题 **dtutil Utility** 中查看 [Encrypt](../../integration-services/dtutil-utility.md)选项的映射，然后确定要用作所选 **ProtectionLevel** 属性的值的相应整数。  
  
3.  打开命令提示符窗口。  
  
4.  在命令提示符下，导航到您要为其设置 **ProtectionLevel** 属性的包所在的文件夹。  
  
     下面步骤中所示的语法示例假设此文件夹是当前文件夹。  
  
5.  使用与下列示例之一相类似的命令，设置或更改包的保护级别。  
  
    -   下面的命令将文件系统中的单个包的 **ProtectionLevel** 属性设置为级别 2“使用密码加密敏感数据”，密码为“strongpassword”：  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   下面的命令将文件系统中特定文件夹内所有包的 **ProtectionLevel** 属性设置为级别 2“使用密码加密敏感数据”，密码为“strongpassword”：  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         如果您在批文件中使用类似的命令，则请输入文件占位符“%f”作为批文件中的“%%f”。  
  
## 另请参阅  
 [dtutil 实用工具](../../integration-services/dtutil-utility.md)  
  
  