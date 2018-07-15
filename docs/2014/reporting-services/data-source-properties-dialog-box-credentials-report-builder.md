---
title: 数据源属性对话框中，凭据 （报表生成器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10017"
ms.assetid: 4531f09f-d653-4c05-a120-d7788838bc99
caps.latest.revision: 11
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c0b6689c1a75cfc9354f8c47532d0ed773f3c6e5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238587"
---
# <a name="data-source-properties-dialog-box-credentials-report-builder"></a>“数据源属性”对话框 -&gt;“凭据”（报表生成器）
  在 **“数据源属性”** 对话框中选择 **“凭据”** 可以显示和修改用于连接到报表中的嵌入数据源的凭据。 您所提供的凭据用于访问数据源以便预览报表。 有关凭据的详细信息，请参阅 [在报表生成器中指定凭据](../../2014/reporting-services/specify-credentials-in-report-builder.md)。  
  
## <a name="options"></a>“常规”  
 **使用 Windows 身份验证 （集成安全性）**  
 选择此选项可以使用 Windows 身份验证。  
  
 **使用此用户名和密码**  
 选择此选项可以提供特定用户名和密码。 对于嵌入数据源，在将报表服务器项目发布到目标服务器时，用户名和密码将保存为数据库的存储凭据。 如果要将用户名和密码用作 Windows 凭据，则可以在目标服务器上更改已发布共享数据源的属性。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]文档中的[创建、删除或修改共享数据源（报表管理器）](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)。  
  
 **用户名**  
 键入用于登录数据源的用户名。  
  
 **密码**  
 键入用于登录数据源的密码。  
  
 **提示输入凭据**  
 选择此选项可以在报表运行时提示输入凭据。  
  
 **输入提示字符串**  
 键入用于指示用户提供数据源登录凭据的语句。  
  
 **无凭据**  
 选择此选项可指定不向数据源提供任何凭据。 仅当数据源不接受凭据，或者要通过其他方式传递凭据时，才使用此选项。  
  
 对于某些数据扩展插件，必须在报表服务器上配置无人参与的执行帐户。  
  
 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 文档中的[从外部数据源中添加数据(SSRS)](report-data/add-data-from-external-data-sources-ssrs.md)和 [配置无人参与的执行帐户（SSRS 配置管理器）](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)中相应数据源类型的主题。  
  
## <a name="see-also"></a>请参阅  
 [用于对话框、窗格和向导的报表生成器帮助](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [“数据源属性”对话框 ->“常规”（报表生成器）](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md)   
 [添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
