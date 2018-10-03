---
title: “浏览所有主体”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 06f636c920ed86313a6e8954af9151fa401e8bf7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788805"
---
# <a name="browse-all-principals-dialog-box"></a>“浏览所有主体”对话框
  使用 **“浏览所有主体”** 对话框可以选择某一数据库主体以便更改该主体对所选项目或者所选文件夹中包含的所有项目的权限。  
  
 **您希望做什么？**  
  
-   [打开“浏览所有主体”对话框](#open_dialog)  
  
-   [配置选项](#options)  
  
##  <a name="open_dialog"></a> 打开“浏览所有主体”对话框  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。  
  
     您在连接到承载 SSISDB 目录的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例。  
  
2.  在对象资源管理器中，展开树以便显示 **“Integration Services 目录”** 节点。  
  
3.  展开 **“SSISDB”** 节点。  
  
4.  若要更改该主体对所选文件夹中包含的所有项目的权限，请右键单击该文件夹，然后单击“属性”。  
  
     若要更改该主体对所选项目的权限，请展开包含该项目的文件夹，右键单击该项目，然后单击“属性”。  
  
5.  选择 **“权限”** 页，然后单击 **“浏览”**。  
  
##  <a name="options"></a> 配置选项  
 此页显示来自 SSISDB 数据库的目录视图 sys.database_principals 的主体。  
  
 选择主体后，在您单击 **“确定”** 并且关闭 **“浏览所有主体”** 对话框时，会将这些主体添加到父对话框的 **“权限”** 页上的 **“登录名或角色”** 列表中。 在将主体添加到 **“登录名或角色”** 列表后，您可以更改该主体对所选项目的权限。  
  
 **选择列**  
 选择此选项可以将主体添加到父对话框的“权限”页上的“登录名或角色”列表中。  
  
 **图标列**  
 与主体的“类型”相对应的图标。  
  
 **名称**  
 主体的名称。  
  
 **类型**  
 主体的类型。 常见类型如下：  
  
-   SQL 用户  
  
-   Windows 用户  
  
-   数据库角色  
  
  
