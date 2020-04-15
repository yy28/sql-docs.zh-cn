---
title: 处理更新语句的选择 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 904028cd7b3798fcac8f9e5afa6186fae3e9fa29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308008"
---
# <a name="processing-select-for-update-statements"></a>处理 SELECT FOR UPDATE 语句
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 为了达到最大的互操作性，应用程序应生成结果集，这些结果集将通过执行**SELECT FOR 更新**语句来使用定位的更新语句进行更新。 尽管游标库不需要这样做，但大多数支持定位更新语句的数据源都需要它。  
  
 游标库忽略"选择更新"语句的**FOR 更新**子句中的列;因此，游标库将忽略"**选择更新"** 语句中的列。在将语句传递给驱动程序之前，它会删除此子句。 在游标库中，SQL_ATTR_CONCURRENCY语句属性以及上一节中提及的限制控制是否可以更新结果集中的列。
