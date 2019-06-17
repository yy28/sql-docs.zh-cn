---
title: 存储过程参数限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dc74811bf6cead91850ebd3fcaa8cf64025c80d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270858"
---
# <a name="stored-procedure-parameter-limitations"></a>存储过程参数限制
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 当运行 Oracle 的存储过程，利用 10 或多个输出参数时，存储的过程调用将失败，从而导致访问冲突或 ActiveX 数据对象 (ADO) 错误。 使用 Microsoft ODBC Driver for Oracle 版本 8.0.4.0.0 和 8.0.4.0.4 Oracle 客户端软件可以发生该错误。  
  
 若要更正此问题，必须升级到版本 8.0.4.2.0 或更高版本的 Oracle 客户端软件。 有关详细信息联系 Oracle Corporation[修补程序](../../odbc/microsoft/oracle-software-patches.md)。  
  
> [!NOTE]  
>  与早期版本的 Oracle 客户端软件版本 8.0.3.0.0 不会出现此问题。
