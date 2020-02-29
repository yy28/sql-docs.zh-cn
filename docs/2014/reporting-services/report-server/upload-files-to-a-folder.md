---
title: 将文件上载到文件夹 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
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
manager: kfile
ms.openlocfilehash: e0bb599b49235cc68fdc7cfa2c74e7b15f6c1c4d
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177162"
---
# <a name="upload-files-to-a-folder"></a>将文件上载到文件夹
  您可以从文件系统上载文件，然后将其作为托管项存储在报表服务器数据库中。 上载文件时的情况因文件类型而异。

-   上载 .rdl 文件相当于发布报表。

-   上载其他任何文件会将该文件作为单个二进制对象添加到报表服务器数据库中。 这些文件作为资源发布到报表服务器。 资源可以是任意类型的文件。 如果文件扩展名与某已知的 MIME 类型相符，则将使用该 MIME 类型的图标来标识资源类型。 否则，将使用通用文件图标表示资源。

> [!NOTE]
>  不能上载报表数据源 (.rds) 文件来创建共享数据源。 .rds 文件仅用于报表设计器中。 对于通过报表管理器定义和管理的共享数据源项，.rds 文件不提供相关内容。 作为上载的替代方法，可以编写一个基于 .rds 文件创建共享数据源的脚本。

 上载项的最大文件大小由 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]确定。 默认情况下，最大大小为 4 MB。

 上载到报表服务器数据库的文件将使用以下图标直观地显示在文件夹层次结构中：

 ![报表图标](../media/hlp-16doc.gif "报表图标")报表图标

 ![模型图标](../media/model-icon.gif "模型图标")报表模型图标

 ![通用资源图标](../media/hlp-16file.gif "通用资源图标")通用资源图标

 上载文件时，文件将始终放入当前所选的文件夹。 您可以首先定位到要包含项的文件夹，也可以先上载文件再将其移至最终位置。

 若要上载文件，请使用报表管理器。 能否将文件上载到报表服务器取决于您的角色分配中包括哪些任务。 如果您使用的是默认安全性，本地管理员可以向报表服务器中添加项。 如果启用了“我的报表”，则拥有“我的报表”文件夹的任何用户都有权将项上载到该文件夹中。 如果您使用自定义角色分配，角色分配必须包括支持管理文件夹的任务。

|要执行此操作|需包含的任务|
|----------------|-------------------------|
|将 .rdl 文件上载到文件夹中|管理报表|
|将任何文件作为二进制对象上载|管理资源|
|查看文件夹的内容|查看资源，查看报表|

## <a name="see-also"></a>另请参阅
 [报表管理器 &#40;SSRS 本机模式&#41;] .。。/report-manager-ssrs-native-mode.md）[授予对本机模式报表服务器](../security/granting-permissions-on-a-native-mode-report-server.md)[任务和权限](../security/tasks-and-permissions.md)的权限[报表管理器 &#40;上传文件或报表&#41;](../reports/upload-a-file-or-report-report-manager.md)


