---
title: 将文件上载到文件夹 | Microsoft Docs
ms.date: 06/17/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
- files [Reporting Services]
- folders [Reporting Services], uploading files to
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d93840b2b1b7354238ccae12ba3a540889038fb2
ms.sourcegitcommit: 1bbbbb8686745a520543ac26c4d4f6abe1b167ea
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2019
ms.locfileid: "67228685"
---
# <a name="upload-files-to-a-folder"></a>将文件上载到文件夹
  您可以从文件系统上载文件，然后将其作为托管项存储在报表服务器数据库中。 上载文件时的情况因文件类型而异。  
  
-   上载 .rdl 文件相当于发布报表。  
  
-   上载其他任何文件会将该文件作为单个二进制对象添加到报表服务器数据库中。 这些文件作为资源发布到报表服务器。 资源可以是任意类型的文件。 如果文件扩展名与某已知的 MIME 类型相符，则将使用该 MIME 类型的图标来标识资源类型。 否则，将使用通用文件图标表示资源。  
  
    >[!NOTE]  
    >不能上载报表数据源 (.rds) 文件来创建共享数据源。 .rds 文件仅用于报表设计器中。 它无法提供通过 Web 门户进行定义和管理的共享数据源项的内容。 作为上载的替代方法，可以编写一个基于 .rds 文件创建共享数据源的脚本。  
  
 已上传的项的最大文件大小为 2 GB，可使用中的 MaxFileSizeMb 属性设置[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。  
  
 上载到报表服务器数据库的文件将使用以下图标直观地显示在文件夹层次结构中：  
  
  ![报告服务器 uploadable 文件图标](../../reporting-services/report-server/media/upload-files-to-a-folder/report-server-uploadable-file-icons.png)
  
 上载文件时，文件将始终放入当前所选的文件夹。 您可以首先定位到要包含项的文件夹，也可以先上载文件再将其移至最终位置。  
  
 若要上传一个文件，请使用 web 门户。 能否将文件上载到报表服务器取决于您的角色分配中包括哪些任务。 如果您使用的是默认安全性，本地管理员可以向报表服务器中添加项。 如果启用了“我的报表”，则拥有“我的报表”文件夹的任何用户都有权将项上载到该文件夹中。 如果您使用自定义角色分配，角色分配必须包括支持管理文件夹的任务。  
  
|执行的操作|需包含的任务|  
|----------------|-------------------------|  
|将 .rdl 文件上载到文件夹中|管理报表|  
|将任何文件作为二进制对象上载|管理资源|  
|查看文件夹的内容|查看资源，查看报表|  
  
## <a name="see-also"></a>另请参阅  
 [报表服务器的 Web 门户（SSRS 本机模式）](../../reporting-services/web-portal-ssrs-native-mode.md)  
 [授予对本机模式报表服务器的权限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [任务和权限](../../reporting-services/security/tasks-and-permissions.md)   
 [在报表服务器中上传文件或报表](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)   
  