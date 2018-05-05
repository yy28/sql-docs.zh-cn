---
title: 释放描述符 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c96d5b654d8331f95e3abbe8a3aa8b563bf7a63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="freeing-descriptors"></a>释放描述符
显式分配的描述符可以是通过调用显式释放或者**SQLFreeHandle**与*HandleType*的 SQL_HANDLE_DESC，还是隐式地释放时的连接句柄。 当释放显式分配的描述符，向其自动应用的释放的描述符恢复为隐式为其分配的描述符中的所有语句句柄。  
  
 可以只是在调用释放隐式分配的描述符**SQLDisconnect**，丢弃任何语句或描述符打开连接，或通过调用**SQLFreeHandle**与*HandleType* SQL_HANDLE_STMT 语句句柄和与语句关联的所有隐式分配的描述符的免费。 不能被隐式分配的描述符释放通过调用**SQLFreeHandle**与*HandleType* SQL_HANDLE_DESC。  
  
 即使释放，隐式分配的描述符就保持有效，和**SQLGetDescField**可以调用它的字段。
