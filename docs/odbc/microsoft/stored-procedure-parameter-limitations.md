---
title: 存储过程参数限制 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbd748884575791d5f170e95bc5aa465b61624b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299197"
---
# <a name="stored-procedure-parameter-limitations"></a>存储过程参数限制
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 当运行使用 10 个或更多输出参数的 Oracle 存储过程时，存储过程调用将失败，从而导致访问冲突或 ActiveX 数据对象 （ADO） 错误。 当使用适用于 Oracle 的 Microsoft ODBC 驱动程序（适用于 Oracle 客户端软件的版本 8.0.4.0.0 和 8.0.4.0.4）时，可能会发生这种情况。  
  
 要更正此问题，必须将 Oracle 客户端软件升级到版本 8.0.4.2.0 或更高版本。 有关[修补程序](../../odbc/microsoft/oracle-software-patches.md)的更多信息，请联系甲骨文公司。  
  
> [!NOTE]  
>  早期发布 Oracle 客户端软件版本 8.0.3.0.0 时不会出现此问题。
