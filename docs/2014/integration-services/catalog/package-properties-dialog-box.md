---
title: “包属性”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageprop.general.f1
- sql12.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 76f1c8e33bf8675e6306857b8a6ec9f5220c2985
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439064"
---
# <a name="package-properties-dialog-box"></a>“包属性”对话框
  使用 **“包属性”** 对话框可以查看在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上存储的包的属性。  
  
 有关详细信息，请参阅 [Integration Services (SSIS) 服务器](integration-services-ssis-server-and-catalog.md)。  
  
 **您希望做什么？**  
  
-   [打开“包属性”对话框](#open_dialog)  
  
-   [配置选项](#options)  
  
##  <a name="open-the-package-properties-dialog-box"></a><a name="open_dialog"></a> 打开“包属性”对话框  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。  
  
     正在连接到承载 SSISDB 数据库的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例。  
  
2.  在对象资源管理器中，展开树以便显示 **“Integration Services 目录”** 节点。  
  
3.  展开 **“SSISDB”** 节点。  
  
4.  展开包含您要查看其属性的包的文件夹。  
  
5.  右键单击该包，然后选择“属性”  。  
  
##  <a name="configure-the-options"></a><a name="options"></a> 配置选项  
 使用 **“常规”** 页可以查看所选包的属性。  
  
 “常规”  页上的所有属性都是只读的。  
  
 **名称**  
 显示包的名称。  
  
 **标识符**  
 列出包 ID。  
  
 **入口点**  
 值 `True` 表示直接启动包。 值 `False` 表示该包由另一个包通过执行包任务启动。 默认值为 `True`。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中为父包和子包设置此属性，方法是在解决方案资源管理器中右键单击包，然后单击“入口点包”  。  
  
 **说明**  
 显示包的可选说明。  
  
  
