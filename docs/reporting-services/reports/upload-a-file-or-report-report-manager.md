---
title: 在报表管理器中上传文件或报表 | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
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
ms.openlocfilehash: b54290c582dab62b7e0f5b8a1cb7ca4dd2eb642c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65573302"
---
# <a name="upload-a-file-or-report-in-the-report-server"></a>在报表管理器中上传文件或报表
报表服务器的 Web 门户提供上传功能，以便可以将报表和其他文件添加到报表服务器而不必从客户端应用程序发布这些项。 从文件系统上载的文件会存储为报表服务器上的项。 所上载的文件类型决定存储方式：  
  
-   .rdl 文件存储为分页报表。  
  
-   包括共享数据源 (.rds) 文件在内的所有其他文件都上载为资源。 报表服务器不会处理资源，但是如果报表服务器支持 MIME 文件类型，则可以通过 Web 门户来查看资源。  
  
### <a name="to-upload-a-file-or-report"></a>上载文件或报表  
  
1.  在 Web 门户中，单击“上传”  。  
  
4.  浏览到想要上传的文件。 可以上载报表定义文件、图像、文档或任何要在报表服务器上可用的文件。  
  
5.  键入新项的名称。 项名称可以包括空格，但不能包括保留字符：\; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|。  
  
6.  若要用新项替换现有项，请选择 **“如果该项已存在，则覆盖该项”** 。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅   
[创建、修改和删除共享数据源](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)
[将文件上传到文件夹](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  
