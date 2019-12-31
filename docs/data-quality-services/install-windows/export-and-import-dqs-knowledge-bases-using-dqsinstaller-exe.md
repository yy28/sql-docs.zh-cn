---
title: Export and Import DQS Knowledge Bases Using DQSInstaller.exe
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 8234c63b-a018-4e55-8184-9a6bdf03274d
author: swinarko
ms.author: sawinark
ms.openlocfilehash: bb2f2a1a1e6aa9b63478b95d7f802e3df7cd127c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254781"
---
# <a name="export-and-import-dqs-knowledge-bases-using-dqsinstallerexe"></a>Export and Import DQS Knowledge Bases Using DQSInstaller.exe

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  对于现有的 DQS 安装，您可以从命令提示符运行 DQSInstaller.exe 文件，以便一次性将 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 中的所有知识库导出到 DQS 备份文件 (.dqsb)，并在稍后使用 .dqsb 文件一次性将所有知识库导入其他 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 。 有关从命令提示符运行 DQSInstaller.exe 的详细信息，请参阅 [从命令提示符运行 DQSInstaller.exe](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#CommandPrompt) 中的 [运行 DQSInstaller.exe 以便完成数据质量服务器安装](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)。  
  
 利用此功能，您可以一次性对 *中的* 所有 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 知识库进行备份，而不必使用 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]单独将每个知识库导出到 .dqs 文件。 同样，您可以一次性将 *所有* 知识库从备份文件导入其他 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] ，而不必使用 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]从 .dqs 文件单独导入每个知识库。 当在计算机上卸载 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] ，然后将其重新安装到其他计算机上时，此功能对于备份和还原知识库特别有用。 您可以轻松地将现有 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安装中的所有知识库导出到 DQS 备份文件 (.dqsb)，然后再在其他计算机上安装 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 之后从该备份文件导入所有知识库。  
  
##  <a name="export"></a>将知识库导出到 dqsbackup.dqsb 文件  
 您可以随时导出或在卸载 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 时导出现有 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]中的所有知识库。  
  
-   若要将 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 中的所有知识库导出到 DQS 备份文件 (.dqsb)，请通过命令提示符使用 `exportkbs` 参数并使用要将知识库导出到的位置的完整路径和文件名来运行 DQSInstaller.exe。 例如，将所有知识库导出到 C: 驱动器中的 DQSBackup.dqsb 文件：  
  
    ```  
    dqsinstaller.exe -exportkbs c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  如果提供的文件名在指定位置已存在，则安装程序会提示您是否要覆盖该文件。  
  
-   若要在卸载 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]时将所有知识库导出到 DQS 备份文件，请通过命令提示符使用 `uninstall` 并使用要将知识库导出到的位置的完整路径和文件名来运行 DQSInstaller.exe。 例如，将所有知识库导出到 C: 驱动器中的 DQSBackup.dqsb 文件，然后卸载 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]：  
  
    ```  
    dqsinstaller.exe -uninstall c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  如果在使用 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 参数从命令提示符卸载 `uninstall` 时未指定 DQS 备份文件的完整路径和文件名，则会显示一条声明将删除所有知识库的消息，并允许您选择是否继续执行卸载过程。  
  
##  <a name="import"></a>从 dqsbackup.dqsb 文件导入知识库  
 完成 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安装后，您可以从 DQS 备份文件 (.dqsb) 导入所有知识库。 若要导入知识库，您必须具有有效的 DQS 备份文件 (.dqsb)。  
  
 通过命令提示符使用 `importkbs` 参数并使用要从中导入知识库的位置的完整路径和文件名来运行 DQSInstaller.exe 文件。 例如，从 C: 驱动器中的 DQSBackup.dqsb 文件导入所有知识库：  
  
```  
dqsinstaller.exe -importkbs c:\DQSBackup.dqsb  
```  
  
 如果 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 中存在使用要导入的知识库的名称的知识库，则导入的知识库名称将追加一条下划线 (_)，后跟从 1 开始的整数值。 例如，如果“CompanyName”域重复，则导入的域名称将为“CompanyName_1”。  
  
## <a name="see-also"></a>另请参阅  
 [运行 Dqsinstaller.exe 以完成数据质量服务器安装](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)   
 [安装 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [将知识库导出到 dqs 文件](../../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)   
 [从 dqs 文件导入知识库](../../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)  
  
  
