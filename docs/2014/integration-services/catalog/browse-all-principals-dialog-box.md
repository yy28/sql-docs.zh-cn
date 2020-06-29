---
title: “浏览所有主体”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: feff922ac12e46a8b78f30ca46bc02a4fd23b4f6
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439114"
---
# <a name="browse-all-principals-dialog-box"></a>“浏览所有主体”对话框
  使用“浏览所有主体”对话框选择数据库主体，以更改所选项目或所选文件夹中包含的所有项目的主体权限  。  
  
 **您希望做什么？**  
  
-   [打开“浏览所有主体”对话框](#open_dialog)  
  
-   [配置选项](#options)  
  
##  <a name="open-the-browse-all-principals-dialog-box"></a><a name="open_dialog"></a> 打开“浏览所有主体”对话框  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。  
  
     正在连接到托管 SSISDB 目录的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例。  
  
2.  在对象资源管理器中，展开树以便显示 **“Integration Services 目录”** 节点。  
  
3.  展开 **“SSISDB”** 节点。  
  
4.  要更改所选文件夹中包含的所有项目的主体权限，请右键单击该文件夹，然后单击“属性”  。  
  
     要更改所选文件的主体权限，请扩展包含该项目的文件夹，右键单击该项目，然后单击“属性”  。  
  
5.  选择 **“权限”** 页，然后单击 **“浏览”** 。  
  
##  <a name="configure-the-options"></a><a name="options"></a> 配置选项  
 此页显示来自 SSISDB 数据库的目录视图 sys.database_principals 的主体。  
  
 选择主体后，在您单击 **“确定”** 并且关闭 **“浏览所有主体”** 对话框时，会将这些主体添加到父对话框的 **“权限”** 页上的 **“登录名或角色”** 列表中。 在将主体添加到 **“登录名或角色”** 列表后，您可以更改该主体对所选项目的权限。  
  
 **选择列**  
 选择此选项可以将主体添加到父对话框的“权限”页上的“登录名或角色”   列表中。  
  
 **图标列**  
 与主体的  “类型”相对应的图标。  
  
 **名称**  
 主体的名称。  
  
 类型   
 主体的类型。 常见类型如下：  
  
-   SQL 用户  
  
-   Windows 用户  
  
-   数据库角色  
  
  
