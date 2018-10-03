---
title: 共享的数据源属性对话框中，凭据 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shareddatasource.credentials.f1
ms.assetid: c08d1a5f-206b-4d53-ab1a-368b651ee5bb
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a6546a9b38c8f12e493ea9fa47741fa56c9fab79
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171069"
---
# <a name="shared-data-source-properties-dialog-box-credentials"></a>“共享数据源属性”对话框 -&gt;“凭据”
  在 **“共享数据源属性”** 对话框中选择 **“凭据”** 可以显示和修改凭据以便连接到报表中的共享数据源。 您所提供的凭据用于访问数据源和缓存数据副本以便进行报表预览。 有关如何缓存预览数据的详细信息，请参阅 [预览报表](reports/previewing-reports.md)。 有关凭据的详细信息，请参阅 [指定报表数据源的凭据和连接信息](report-data/specify-credential-and-connection-information-for-report-data-sources.md)。  
  
## <a name="options"></a>选项  
 **使用 Windows 身份验证 （集成安全性）**  
 选择此选项可以使用 Windows 身份验证。  
  
 **使用此用户名和密码**  
 选择此选项可以提供特定用户名和密码。 对于共享数据源，当您将报表服务器项目发布到目标服务器时，用户名和密码将作为数据库的存储凭据保存。 如果要将用户名和密码用作 Windows 凭据，则可以在目标服务器上编辑已发布共享数据源的属性。 有关详细信息，请参阅[创建、删除或修改共享数据源（报表管理器）](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)。  
  
 **用户名**  
 键入登录数据源时要使用的用户名。  
  
 **密码**  
 键入登录数据源时要使用的密码。  
  
 **提示输入凭据**  
 选择此选项可以在运行报表时提示输入凭据。  
  
 **输入提示字符串**  
 键入用于指示用户提供数据源登录凭据的语句。  
  
 **无凭据**  
 选择此选项可指定不向数据源提供任何凭据。 仅当数据源不接受凭据，或者要通过其他方式传递凭据时，才使用此选项。  
  
## <a name="see-also"></a>请参阅  
 [数据连接、 数据源和 Reporting Services 中的连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [为报表数据源指定凭据和连接信息](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [“共享数据源属性”对话框 ->“常规”](../../2014/reporting-services/shared-data-source-properties-dialog-box-general.md)  
  
  
