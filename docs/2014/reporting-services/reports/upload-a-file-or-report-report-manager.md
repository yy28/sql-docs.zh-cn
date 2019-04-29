---
title: 上传文件或报表（报表管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6f6cfea7ec9e19a97c94b636f3233bdf73238668
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63067563"
---
# <a name="upload-a-file-or-report-report-manager"></a>上载文件或报表（报表管理器）
  报表管理器提供上载功能，因而您可以将报表、模型以及其他文件添加到报表服务器而不必从客户端应用程序发布这些项。 从文件系统上载的文件会存储为报表服务器上的项。 所上载的文件类型决定存储方式：  
  
-   .rdl 文件存储为报表。  
  
-   .smdl 文件存储为报表模型。  
  
-   包括共享数据源 (.rds) 文件在内的所有其他文件都上载为资源。 报表服务器不会处理资源，但是如果报表服务器支持 MIME 文件类型，则可以通过报表管理器来查看资源。  
  
### <a name="to-upload-a-file-or-report"></a>上载文件或报表  
  
1.  启动 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
2.  在报表管理器中，导航到 **“内容”** 页。 导航到要向其中添加项的文件夹。  
  
3.  单击 **“上载文件”**。  
  
4.  单击 **“浏览”** 以选择要上载的文件。 可以上载报表定义文件、图像、文档或任何要在报表服务器上可用的文件。  
  
5.  键入新项的名称。 项名称可以包括空格，但不能包括保留字符: ; ? : \@ & = + , $ / * \< > |.  
  
6.  若要用新项替换现有项，请选择 **“如果该项已存在，则覆盖该项”**。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [创建、删除或修改共享数据源（报表管理器）](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [“内容”页（报表管理器）](../contents-page-report-manager.md)   
 [“上传文件”页（报表管理器）](../upload-file-page-report-manager.md)   
 [将文件上载到文件夹](../report-server/upload-files-to-a-folder.md)  
  
  
