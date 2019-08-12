---
title: SQL Server 中央管理服务器扩展
titleSuffix: Azure Data Studio
description: 安装和使用 Azure Data Studio 的 SQL Server 中央管理服务器扩展（预览版）
ms.custom: seodec18
ms.date: 06/06/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 03edfc5b6d95c5cd6497d96d7014641f3032fb84
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959207"
---
# <a name="sql-server-central-management-servers-extension-preview"></a>SQL Server 中央管理服务器扩展（预览版）
使用中央管理服务器扩展，用户可以存储组织到一个或多个组中的 SQL Server 实例列表。 使用 CMS 组执行的操作将作用于服务器组中的所有服务器。

此体验目前处于初始预览阶段。 请在[此处](https://github.com/microsoft/azuredatastudio/issues)报告问题和功能请求。

![CMS 扩展](media/sql-server-cms-extension/cms-list.png)

## <a name="install-the-sql-server-central-management-servers-extension"></a>安装 SQL Server 中央管理服务器扩展

1. 若要打开扩展管理器并访问可用扩展，请选择扩展图标，或在“视图”菜单中选择“扩展”   。
2. 选择可用的扩展以查看其详细信息。
1. 选择所需的扩展（SQL Server 中央管理服务器），然后选择“安装”以进行安装  。

### <a name="how-do-i-start-central-management-servers"></a>如何启动中央管理服务器？
 可以通过单击“连接”图标 (Ctrl/Cmd + G) 来查看中心管理服务器。 首次下载扩展时，CMS 视图将被最小化，可单击“中央管理服务器”将其打开 

## <a name="next-steps"></a>后续步骤
若要从概念上了解有关中央管理服务器的详细信息，[请参阅此处](https://docs.microsoft.com/sql/ssms/register-servers/create-a-central-management-server-and-server-group)。


