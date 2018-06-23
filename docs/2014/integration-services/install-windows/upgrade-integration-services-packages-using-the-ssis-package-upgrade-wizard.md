---
title: 使用 SSIS 包升级向导升级 Integration Services 包 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services packages, upgrading
- upgrading Integration Services packages
ms.assetid: 9359275a-48f5-4d1e-8ae7-e797759e3ccf
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 44ffe15525667ad907e282efda510a63d347c30e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129700"
---
# <a name="upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard"></a>使用 SSIS 包升级向导升级 Integration Services 包
  您可以将在早期版本的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中创建的包升级为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 格式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包升级向导来帮助完成此过程。 由于可以将该向导配置为备份原始包，因此如果您遇到升级困难，可以继续使用这些原始包。  
  
 安装 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 时，将安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包升级向导。  
  
> [!NOTE]  
>  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 的 Standard Edition、Enterprise Edition 和 Developer Edition 提供了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]包升级向导。  
  
 有关如何升级 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的详细信息，请参阅 [升级 Integration Services 包](upgrade-integration-services-packages.md)。  
  
 本主题的其余部分介绍了如何运行向导和备份原始包。  
  
## <a name="running-the-ssis-package-upgrade-wizard"></a>运行 SSIS 包升级向导  
 您可以从 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]或在命令提示符下运行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]包升级向导。  
  
#### <a name="to-run-the-wizard-from-sql-server-data-tools"></a>从 SQL Server Data Tools 运行向导  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，创建或打开一个 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，右键单击“SSIS 包”节点，然后单击“升级所有包”来升级该节点下的所有包。  
  
    > [!NOTE]  
    >  打开包含[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 包的 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 项目时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将自动打开 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包升级向导。  
  
#### <a name="to-run-the-wizard-from-sql-server-management-studio"></a>从 SQL Server Management Studio 运行向导  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，展开“已存储的包”节点，接着右键单击“文件系统”节点或“MSDB”节点，然后单击“升级包”。  
  
#### <a name="to-run-the-wizard-at-the-command-prompt"></a>在命令提示符下运行向导  
  
-   在命令提示符下运行的 SSISUpgrade.exe 文件**C:\Program Files\Microsoft SQL Server\120\DTS\Binn**文件夹。  
  
## <a name="backing-up-the-original-packages"></a>备份原始包  
 若要备份原始包，必须将原始包和已升级包存储在文件系统的同一文件夹中。 根据向导的运行方式，可以自动选择该存储位置。  
  
-   从 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 运行 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]包升级向导时，该向导会自动将原始包和已升级包存储在文件系统的同一文件夹中。  
  
-   从 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 或在命令提示符下运行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 包升级向导时，可以为原始包和已升级包指定不同的存储位置。 若要备份原始包，请确保指定将原始包和已升级包存储在文件系统的同一文件夹中。 如果指定任何其他存储选项，则向导将无法备份原始包。  
  
 向导备份原始包时，此向导将在 **SSISBackupFolder** 文件夹中存储该原始包的副本。 向导会创建此 **SSISBackupFolder** 文件夹，将其作为包含原始包和已升级包的文件夹的子文件夹。  
  
#### <a name="to-back-up-the-original-packages-in-sql-server-management-studio-or-at-the-command-prompt"></a>在 SQL Server Management Studio 中或在命令提示符下备份原始包  
  
1.  将原始包保存到文件系统上的某个位置。  
  
    > [!NOTE]  
    >  向导中的备份选项只能用于已存储到文件系统中的包。  
  
2.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中或在命令提示符下，运行 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包升级向导。  
  
3.  在向导的 **“选择源位置”** 页上，将 **“包源”** 属性设置为 **“文件系统”**。  
  
4.  在向导的“选择目标位置”页上，选择“保存到源位置”，从而将已升级的包保存到与原始包相同的位置。  
  
    > [!NOTE]  
    >  仅当将已升级包存储在与原始包相同的文件夹中时，向导中的备份选项才可用。  
  
5.  在向导的 **“选择包管理选项”** 页上，选择 **“备份原始包”** 选项。  
  
#### <a name="to-back-up-the-original-packages-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中备份原始包  
  
1.  将原始包保存到文件系统上的某个位置。  
  
2.  在向导的 **“选择包管理选项”** 页上，选择 **“备份原始包”** 选项。  
  
    > [!WARNING]  
    >  **备份原始包**打开时不会显示选项[!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]或[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]项目中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，因为将自动启动该向导。  
  
3.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，运行 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包升级向导。  
  
  