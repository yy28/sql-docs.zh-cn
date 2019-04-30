---
title: VARCHAR 列大小 （Oracle ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db2871324f92ef6d84a8bf8313db105489100a96
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232164"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 列大小（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 在 Oracle8，VARCHAR 列的最大大小已增加从 2000年到 4000 字节。 Oracle 7.3.x 版客户端软件有没有办法将绑定的参数值大于 2000 个字节。 因此，如果使用的大小超过 2000 个字节的 VARCHAR 列创建一个表，将无法执行参数化的插入、 更新和删除，对其具有超过 2000年字节的限制的客户端软件的数据的查询。 Oracle ODBC 驱动程序和 OLE DB Provider for Oracle 都使用参数化的插入、 更新、 删除和查询，因为它们将在这种情况下报告 ORA 01026 错误。 Oracle 客户端软件通过强制实施的限制范围内的数据将起作用。 若要避免此 2000年字节的限制，则必须在客户端软件升级到 Oracle8 (8.0.4.1.1c 或更高版本)。
