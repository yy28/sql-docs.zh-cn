---
title: “包属性”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageprop.general.f1
- sql13.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8e392e406ce9c17cc24f57a22cef03de2c363a21
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289049"
---
# <a name="package-properties-dialog-box"></a>“包属性”对话框
  使用 **“包属性”** 对话框可以查看在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上存储的包的属性。  
  
 有关详细信息，请参阅 [Integration Services (SSIS) 服务器](../integration-services-ssis-packages.md)。  
  
 **您希望做什么？**  
  
-   [打开“包属性”对话框](#open_dialog)  
  
-   [配置选项](#options)  
  
##  <a name="open_dialog"></a> 打开“包属性”对话框  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。  
  
     正在连接到承载 SSISDB 数据库的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例。  
  
2.  在对象资源管理器中，展开树以便显示 **“Integration Services 目录”** 节点。  
  
3.  展开 **“SSISDB”** 节点。  
  
4.  展开包含您要查看其属性的包的文件夹。  
  
5.  右键单击该包，然后选择“属性”。  
  
##  <a name="options"></a> 配置选项  
 使用 **“常规”** 页可以查看所选包的属性。  
  
 “常规”页上的所有属性都是只读的。  
  
 **名称**  
 显示包的名称。  
  
 **Identifier**  
 列出包 ID。  
  
 **入口点**  
 **True** 的值表示将直接启动包。 值 **False** 表示该包由另一个包通过执行包任务启动。 默认值是 **True**秒。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中为父包和子包设置此属性，方法是在解决方案资源管理器中右键单击包，然后单击“入口点包”。  
  
 **Description**  
 显示包的可选说明。  
  
  
