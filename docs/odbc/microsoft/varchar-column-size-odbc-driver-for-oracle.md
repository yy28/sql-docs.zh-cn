---
description: VARCHAR 列大小（Oracle ODBC 驱动程序）
title: 用于 Oracle)  (ODBC 驱动程序的 VARCHAR 列大小 |Microsoft Docs
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
ms.openlocfilehash: c490487f0edb15fe7d7165b79c4c5f1730a0dd22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449059"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 列大小（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 在 Oracle8 中，VARCHAR 列的最大大小增加了2000到4000个字节。 Oracle 7.3. x 客户端软件无法绑定大于2000字节的参数值。 因此，如果您创建一个包含大于2000字节的 VARCHAR 列的表，则您将无法对其执行参数化插入、更新、删除和查询，其数据超出了客户端软件的2000字节限制。 由于用于 oracle 的 ODBC 驱动程序和用于 Oracle 的 OLE DB 提供程序都使用参数化插入、更新、删除和查询，因此在这种情况下，它们将报告 TNSNAMES.ORA-01026 错误。 在 Oracle 客户端软件强制实施的限制范围内的数据将起作用。 若要避免此2000字节的限制，必须将客户端软件升级到 Oracle8 (8.0.4.1.1 c 或更高版本) 。
