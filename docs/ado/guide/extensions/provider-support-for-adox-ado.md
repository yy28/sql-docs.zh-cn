---
title: 用于 ADOX (ADO) 提供程序支持 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48f0e58ce794f53a123267b664e8c4c933976fe7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="provider-support-for-adox-ado"></a>用于 ADOX (ADO) 提供程序支持
ADOX 的某些功能不受支持，具体取决于 OLE DB 数据访问接口。 完全支持 ADOX [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)。 不支持的功能与[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)、 [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)，或[Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)是下表中列出。 任何其他 Microsoft OLE DB 提供程序不支持 ADOX。  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Microsoft OLE DB Provider for SQL Server  
  
|对象或集合|使用限制|  
|--------------------------|-----------------------|  
|**表**集合|引用现有对象时，则属性是读/写对象创建之前，只读的。|  
|**视图**集合|**视图**不支持。|  
|**过程**集合|**追加**和**删除**不支持的方法。|  
|**过程**对象|**命令**不支持属性。|  
|**密钥**集合|**追加**和**删除**不支持的方法。|  
|**用户**集合|**用户**不支持。|  
|**组**集合|**组**不支持。|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Microsoft OLE DB Provider for ODBC  
  
|对象或集合|使用限制|  
|--------------------------|-----------------------|  
|**目录**对象|**创建**不支持方法。|  
|**表**集合|**追加**和**删除**不支持的方法。 引用现有对象时，则属性是读/写对象创建之前，只读的。|  
|**过程**集合|**追加**和**删除**不支持的方法。|  
|**过程**对象|**命令**不支持属性。|  
|**索引**集合|**追加**和**删除**不支持的方法。|  
|**密钥**集合|**追加**和**删除**不支持的方法。|  
|**用户**集合|**用户**不支持。|  
|**组**集合|**组**不支持。|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Microsoft OLE DB Provider for Oracle  
  
|对象或集合|使用限制|  
|--------------------------|-----------------------|  
|**目录**对象|**创建**不支持方法。|  
|**表**集合|**追加**和**删除**不支持的方法。 引用现有对象时，则属性是读/写对象创建之前，只读的。|  
|**视图**集合|**追加**和**删除**不支持的方法。|  
|**视图**对象|**命令**不支持属性。|  
|**过程**对象|**追加**和**删除**不支持的方法。|  
|**过程**对象|**命令**不支持属性。|  
|**索引**集合|**追加**和**删除**不支持的方法。|  
|**密钥**集合|**追加**和**删除**不支持的方法。|  
|**用户**集合|**用户**不支持。|  
|**组**集合|**组**不支持。|
