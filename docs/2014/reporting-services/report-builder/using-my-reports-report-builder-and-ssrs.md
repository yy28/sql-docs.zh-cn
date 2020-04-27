---
title: 使用“我的报表”（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 49c3c1da-b106-41f6-9173-16ff225bade8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 410cb4de6b89052493618404df3e595fd6999936
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107579"
---
# <a name="using-my-reports-report-builder-and-ssrs"></a>使用“我的报表”（报表生成器和 SSRS）
  在配置为本机模式的报表服务器上，“我的报表”文件夹是一个个人工作区，您可以用它来存储和处理自己的报表。 其他报表服务器文件夹都是公用文件夹，通常要求用户具有高级权限才能添加或修改文件夹内容。 相反，“我的报表”文件夹则是用户管理的工作区。 您可以添加或删除报表和文件夹，保存带有个性化设置的链接报表。  
  
 从概念上说，“我的报表”文件夹类似于 Windows 文件系统中的“我的文档”文件夹。 尽管每个用户都有一个名为“我的报表”的文件夹，但用户都只能访问各自的相应文件夹。 除了报表服务器管理员之外，其他用户都无法访问您的“我的报表”文件夹中的内容。  
  
 “我的报表”功能是可选的，报表服务器管理员可以禁用此功能。 如果启用此功能，您就会在主文件夹中看到“我的报表”文件夹，可以使用报表管理器或 Web 浏览器访问该文件夹。 有关详细信息，请参阅[在报表管理器中查找和查看报表（报表生成器和 SSRS）](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)。  
  
 在配置为 SharePoint 集成模式的报表服务器上，没有与“我的报表”文件夹等同的项。 有关详细信息，请参阅 [查找、查看和管理报表（报表生成器和 SSRS）](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="ways-to-use-my-reports"></a>使用“我的报表”文件夹的方法  
 在您添加报表、文件夹和其他项之前，“我的报表”为空文件夹。 下面是向“我的报表”文件夹中添加内容的一些方法：  
  
-   创建个人的链接报表，并将其存储在“我的报表”文件夹中。 并非所有的报表都适合链接。 有关详细信息，请参阅 [创建链接报表](../reports/create-a-linked-report.md)。  
  
-   上载报表定义 (.rdl) 文件、报表模型 (.smdl) 文件或文件系统中的其他文件。 您可以上载任何文件，但报表服务器只处理扩展名为 .rdl 或 .smdl 的报表文件。 有关详细信息，请参阅 SQL Server 联机丛书中 [Reporting Services 文档](https://go.microsoft.com/fwlink/?linkid=121312)中的“报表定义”和[上传文件或报表（报表管理器）](../reports/upload-a-file-or-report-report-manager.md)。  
  
-   创建您自己的报表并将其发布到“我的报表”文件夹。 有关详细信息，请参阅[报表设计视图（报表生成器）](report-design-view-report-builder.md)。  
  
 通常，“我的报表”的权限允许您自己管理该文件夹。 但是，最终还是由报表服务器管理员决定用户可以执行哪些任务。 如果您因权限不足而无法使用“我的报表”文件夹，请咨询报表服务器管理员。  
  
## <a name="searching-my-reports"></a>搜索“我的报表”文件夹  
 当您搜索报表服务器数据库时，您的“我的报表”文件夹中的内容也在搜索之列，而其他用户的“我的报表”文件夹中的内容则被排除在外。 搜索结果中将只列出您可以访问的报表。  
  
## <a name="see-also"></a>另请参阅  
 [查找、查看和管理报表（报表生成器和 SSRS）](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
