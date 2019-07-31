---
ms.openlocfilehash: 327fd6bac9bc1036a0dd07f7b955ee92cb7e40c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223542"
---
  从 SQL Server 2005 开始，架构的行为发生了更改。 因此，假设架构与数据库用户等价的代码不再返回正确的结果。 旧目录视图（包括 sysobjects）不应用于曾使用下列任何 DDL 语句的数据库中：CREATE SCHEMA、ALTER SCHEMA、DROP SCHEMA、CREATE USER、ALTER USER、DROP USER、CREATE ROLE、ALTER ROLE、DROP ROLE、CREATE APPROLE、ALTER APPROLE、DROP APPROLE、ALTER AUTHORIZATION。 在这类数据库中，必须改用新目录视图。 新的目录视图将采用在 SQL Server 2005 中引入的使主体和架构分离的方法。 有关目录视图的详细信息，请参阅[目录视图 (Transact-SQL)](../relational-databases/system-catalog-views/catalog-views-transact-sql.md)。
   