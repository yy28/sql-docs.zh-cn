---
title: 释放描述符 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af30ceb29e032764b89aa2069086aa898a7d35db
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305598"
---
# <a name="freeing-descriptors"></a>释放描述符
显式分配的描述符可以通过使用*SQL_HANDLE_DESC 的 HandleType*调用**SQLFreeHandle**或隐式释放连接句柄时显式释放。 释放显式分配的描述符时，释放的描述符应用的所有语句句柄将自动还原到隐式为其分配的描述符。  
  
 隐式分配的描述符只能通过调用**SQLDisconnect**（它丢弃连接上打开的任何语句或描述符）来释放，或者使用*handletype* SQL_HANDLE_STMT 调用**SQLFreeHandle**以释放语句句柄以及与语句关联的所有隐式分配的描述符。 无法通过使用*SQL_HANDLE_DESC的句柄类型*调用**SQLFreeHandle**来释放隐式分配的描述符。  
  
 即使释放，隐式分配的描述符仍然有效 **，SQLGetDescField**也可以在其字段上调用。
