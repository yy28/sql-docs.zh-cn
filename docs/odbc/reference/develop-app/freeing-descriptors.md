---
title: 释放描述符 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe489222c026c1499135b716f0485bb04f51bad9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069774"
---
# <a name="freeing-descriptors"></a>释放描述符
可以是显式分配的描述符是显式释放通过调用**SQLFreeHandle**与*HandleType* SQL_HANDLE_DESC，或隐式时，将释放连接句柄。 显式分配的描述符被释放时，会自动应用的已释放的描述符还原为隐式为其分配的描述符到的所有语句句柄。  
  
 可以只是在调用释放隐式分配的描述符**SQLDisconnect**，可删除的任何语句或描述符打开的连接上，或通过调用**SQLFreeHandle**与*HandleType*为 SQL_HANDLE_STMT 以释放语句句柄和与语句相关联的所有隐式分配的描述符。 隐式分配的描述符不能释放通过调用**SQLFreeHandle**与*HandleType* SQL_HANDLE_DESC。  
  
 释放，即使是隐式分配的描述符保持有效，并**SQLGetDescField**可以调用其字段。
