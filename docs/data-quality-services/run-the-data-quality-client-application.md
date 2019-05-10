---
title: 运行 Data Quality Client 应用程序 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.browseforservers.f1
- sql13.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8df64b4dc6f703751ef68ea72a8bcf9238a365fc
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65487864"
---
# <a name="run-the-data-quality-client-application"></a>运行数据质量客户端应用程序

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  运行 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]，并登录到 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 您必须已通过运行 DQSInstaller.exe 文件完成了 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 安装。 有关详细信息，请参阅 [运行 DQSInstaller.exe 以便完成数据质量服务器安装](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须具有对 DQS_MAIN 数据库授予的三种 DQS 角色（dqs_adminstrator、dqs_kb_editor 或 dqs_kb_operator）中的一种，才能登录到 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。  
  
##  <a name="Run"></a> 运行数据质量客户端  
 若要在安装了 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的计算机上运行它，请执行以下操作：  
  
1.  单击 **“开始”**，指向 **“所有程序”**，依次单击 **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**、 **Data Quality Services**和 **“数据质量客户端”**。  
  
2.  在 **“连接到服务器”** 对话框中：  
  
    1.  指定您要将 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序连接到的服务器。 选择 **(LOCAL)** 以便连接到本地计算机上的 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 。 还可以单击向下箭头并选择“\<浏览网络以查找更多服务器>”，以便连接到其他服务器（或者按名称连接到本地服务器）。 将显示 **“查找服务器”** 对话框。 您可以在 **“本地服务器”** 选项卡或 **“网络服务器”** 选项卡中选择某一服务器。  
  
    2.  若要加密在 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 和 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]之间传输的数据，请单击“选项” ，然后选中“加密连接”  复选框。  
  
3.  单击 **“连接”**。  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕将出现。 有关详细信息，请参阅[数据质量客户端主屏幕](../data-quality-services/data-quality-client-home-screen.md)。  
  
  
