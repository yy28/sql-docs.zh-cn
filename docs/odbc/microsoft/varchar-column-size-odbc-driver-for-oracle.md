---
title: VARCHAR 列大小（Oracle 的 ODBC 驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11e1de3171521c57c80beb207d33e67d26d3e33
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304822"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 列大小（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 在 Oracle8 中，VARCHAR 列的最大大小从 2000 字节增加到 4000 字节。 Oracle 7.3.x 客户端软件无法绑定大于 2000 字节的参数值。 因此，如果创建 VARCHAR 列大于 2000 字节的表，则无法对它执行参数化插入、更新、删除和查询，数据超过客户端软件的 2000 字节限制。 由于 Oracle 的 ODBC 驱动程序和 Oracle 的 OLE DB 提供程序都使用参数化插入、更新、删除和查询，因此在这种情况下，它们将报告 ORA-01026 错误。 在 Oracle 客户端软件强制执行的限制范围内的数据将起作用。 为了避免此 2000 字节限制，必须将客户端软件升级到 Oracle8（8.0.4.1.1c 或更高版本）。
