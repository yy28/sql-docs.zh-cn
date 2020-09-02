---
description: ODBC 测试是一个启用了 ODBC 的应用程序，可用于测试 ODBC 驱动程序和 ODBC 驱动程序管理器。
title: ODBC 测试
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC test [ODBC]
- ODBC drivers [ODBC], testing
- gtrtst32.dll
- gtrts32w.dll [ODBC]
- odbct32w.exe [ODBC]
- odbcte32.exe [ODBC]
- testing ODBC drivers [ODBC]
ms.assetid: 7f13894c-5697-436c-be3d-fe16e1a02325
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39869fe1230be75d9a76e13b8ba3938ec31ee5ee
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288242"
---
# <a name="odbc-test"></a>ODBC 测试

## <a name="about"></a>关于

Microsoft® ODBC 测试是一个启用了 ODBC 的应用程序，可用于测试 ODBC 驱动程序和 ODBC 驱动程序管理器。 ODBC 测试包含在 [Microsoft 数据访问组件 (MDAC) 2.8 软件开发工具包](https://www.microsoft.com/download/details.aspx?id=21995)中。

ODBC 3.51 同时包含 ANSI 和 Unicode 启用版本的 ODBC 测试。 相应的文件如下所示：

- `Odbcte32.exe``Gtrtst32.dll`对于 ANSI 版本，则为。

- `Odbct32w.exe``Gtrts32w.dll`对于 Unicode 版本，则为。

若要使用 ODBC 测试，必须了解 ODBC API、C 语言和 SQL。 有关 ODBC API 的详细信息，请参阅 [Odbc 程序员参考](../odbc/reference/odbc-programmer-s-reference.md)。

本文的此部分中包含的帮助主题现在包含在 ODBC 测试程序中。 打开 `Odbcte32.exe` 或 `Odbct32w.exe` 打开 " **帮助** " 菜单，然后单击 " **帮助主题**"。

请注意，这些应用程序的64位版本（适用于64位 Microsoft Windows 操作系统）具有与32位版本相同的名称，即使它们是单独的文件。 例如，64位版本的 ODBC 测试的 Unicode 版本的名称为 `odbct32w.exe` 。

## <a name="open-source"></a>开源

ODBC 测试是开放源代码。 若要查看代码并自行生成最新版本的 ODBC 测试，请参阅 [GitHub 存储库进行 Odbc 测试](https://github.com/microsoft/ODBCTest)。
