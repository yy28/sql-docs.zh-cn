---
title: MSSQLSERVER 属性的协议（“证书”选项卡）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.computermgr.cert.general.f1
helpviewer_keywords:
- MSSQLSERVER property protocols
ms.assetid: 776addd6-25f3-4875-9a71-064035787090
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 85e7e9cbc454785379fac029cbe970a492e0fffd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47760095"
---
# <a name="protocols-for-mssqlserver-properties-certificate-tab"></a>MSSQLSERVER 属性的协议（“证书”选项卡）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  使用 **“MSSQLSERVER 协议的属性”** 对话框中的 **“证书”** 选项卡可以选择 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]证书，也可以查看证书的属性。 在选择证书之前，所有字段均为空。  
  
 用户的证书存储在本地计算机上。 若要加载供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的证书，您必须在与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务所用的同一用户帐户下运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
## <a name="page-header"></a>页眉  
 **“视图”**  
 通过它可以访问有关证书的其他详细信息。 只有在 **“证书”** 框中选择某个证书后，此选项才可用。 有关证书详细信息的其他信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 文档。  
  
 **Clear**  
 从“证书”框中删除所选证书。  
  
 **证书**  
 由安全提供程序确定的证书名称。 选择某个证书可以在属性网格中查看详细信息。  
  
## <a name="options"></a>选项  
 过期日期  
 证书有效期最后一天的日期。  
  
 友好名称  
 获得证书的个人或证书颁发机构的友好名称或公用名称。  
  
 颁发者  
 有关颁发证书的证书颁发机构的信息。  
  
 颁发给  
 有关证书接收者的信息。  
  
  
