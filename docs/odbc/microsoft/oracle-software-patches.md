---
title: Oracle 软件修补程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], Oraclesoftware patches
- Oracle software patches [ODBC]
ms.assetid: 1275157b-f4e1-4c24-b273-c02555e261c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1fb577e7b08f6ef332ed35f6d275a5f7ce543ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292947"
---
# <a name="oracle-software-patches"></a>Oracle 软件修补程序
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 需要 Oracle 服务器产品和客户端组件的修补程序才能正常工作几个 Microsoft 产品和技术，包括用于 Oracle 的 Microsoft ODBC 驱动程序、Oracle 的 Microsoft OLE DB 提供程序、Internet Information Services （IIS）、组件服务（或 Microsoft 事务服务器，如果使用的是 Windows NT）等。  
  
> [!NOTE]  
>  以下说明可能不完全准确，因为 Oracle FTP 站点可能会发生更改。  
  
### <a name="to-download-the-oracle-software-patches"></a>下载 Oracle 软件修补程序  
  
1.  在 oracle-ftp.oracle.com 连接到公共 FTP 站点。 用户 ID 为 "匿名"，密码为你的电子邮件地址。  
  
2.  导航到以下目录：/server/wgt_tech/server/windowsNT。  
  
3.  若要下载与 Windows 95、Windows 98 和 Windows NT/Windows 2000 最相关的修补程序，请导航到你的 Oracle 版本的的子目录-7.3 或8.0。 这两个子目录是/73patchsets 和/80patchsets。  
  
4.  若要下载 Oracle 网络技术修补程序（SQL * Net 或 Net8），请导航到以下目录：/network。  
  
 从 Web 浏览器访问此 FTP 站点可能不起作用。 如果遇到问题，请尝试使用 "传统" FTP 客户端或使用 DOS 命令提示符。  
  
> [!NOTE]  
>  由于 Oracle 在当前版本中修复了 bug，然后使用软件修补程序将其 retrofits 到早期版本，因此建议下载最新的可用修补程序。 对于 Oracle 服务器客户端组件尤其如此。 如果你对安装这些修补程序有疑问，请联系 Oracle 支持部门。
