---
title: 数据源对象 (TMSL) |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7beabaaf63194cc699c3711a87dd1e59d244c068
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981329"
---
# <a name="datasources-object-tmsl"></a>数据源对象 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  定义到模型期间导入到模型中，或在 DirectQuery 模式下通过传递查询中添加数据，或者使用的数据源的连接。  在 DirectQuery 模式下的模型只能有一个**数据源**对象。  
  
 除非您要创建的替换，或更改数据源对象本身 （如分区脚本） 在脚本中引用的任何数据源必须是现有**数据源**在模型中的对象。  
  
## <a name="object-definition"></a>对象定义  
 所有对象都具有一组通用的属性，包括名称、 类型、 说明、 属性集合和批注。 **数据源**对象还具有以下属性。  
  
 type  
 DataSource 的类型。 目前，唯一有效的值是提供程序 (1)-常规连接字符串。  
  
 connectionString  
 连接字符串的最小日志指定的服务器和数据库，但还可以包括支持外部 RDBMS 中，如数据提供程序或用户帐户的其他属性。 此值是必需的。 请参阅[SqlConnectionStringBuilder 类](https://msdn.microsoft.com/library/ms254500\(v=vs.110\).aspx)有关 SQL Server 的详细信息的数据库连接字符串属性。  
  
 impersonationMode  
 指定 Analysis Services 是否应模拟请求查询的用户标识。 此属性是一个数字值，指定要用于模拟的凭据。 枚举值如下：  
  
-   默认值 (1)-服务器使用它认为不适用于在其中使用模拟上下文的模拟方法。  
  
-   ImpersonateAccount (2)-服务器使用指定的用户帐户。  
  
-   ImpersonateAnonymous (3)-服务器使用匿名用户帐户。  此选项不建议使用，但有时使用 HTTP 访问方案中处理身份验证的自定义应用程序。  
  
-   ImpersonateCurrentUser (4)-服务器使用作为连接客户端的用户帐户。  
  
-   ImpersonateServiceAccount (5) 的服务器使用服务器运行作为用户帐户。  
  
-   ImpersonateUnattendedAccount (6) – 服务器使用无人参与的用户帐户。 这用于在 SharePoint 环境中运行的 Power Pivot 或表格模型。  
  
 如果为受信任委派配置 Analysis Services，DirectQuery 模式下可以使用 impersonateCurrentuser 或  
                      impersonateServiceAccount 如果 Analysis Services 服务帐户的安全上下文中发出查询请求。 请参阅[配置 Analysis Services for Kerberos 约束委派](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)。  
  
 account  
 用于模拟。 一个 Windows 帐户或数据库帐户有效的登录名具有读取权限的外部数据库。  
  
 password  
 提供的帐户的密码加密的字符串。  
  
 maxConnections  
 到数据源的要开启的并发连接的最大数量。  
  
 隔离  
 数据源执行命令时用于隔离的类型。 有效值为 ReadCommitted （1） 或快照 (2)。  
  
 timeout  
 一个整数，指定以秒为单位对数据源执行的命令的超时。  
  
 提供程序  
 一个可选字符串，用于标识托管的数据提供程序连接到关系数据库中，如果未使用的连接字符串上指定的名称。  
  
## <a name="usage"></a>用法  
 **数据源**在中使用对象[Alter 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)，[创建命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)， [CreateOrReplace 命令中&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)，[删除命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)， [Refresh 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)，并[MergePartitions 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md)。  
  
 一个**数据源**对象是一个属性的模型，但也可以指定为数据库对象的模型和数据库之间的一对一映射的属性。  此外指定基于 SQL 的查询的分区**数据源**，只能使用一组缩减的属性。  
  
 在创建时，替换或更改数据源对象，将指定对象定义的所有读写的属性。 省略一个读写属性被视为某一删除操作。  
  
## <a name="examples"></a>示例  
 **示例 1** -连接到*FoodMart*上的命名实例的远程数据库*销售*网络服务器上*Server01*。  
  
```  
"dataSources": [  
      {  
        "name": "SqlServer Server01 FoodMart",  
        "connectionString": "Provider=SQLNCLI11;Data Source=Server01\Sales;Initial Catalog=Foodmart;Integrated Security=SSPI;Persist Security Info=false",  
        "impersonationMode": "impersonateServiceAccount",  
      }  
]  
```  
  
## <a name="full-syntax"></a>完整语法  
 下面是一个模型的数据源对象的架构表示形式。  
  
```  
"dataSources": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "ProviderDataSource object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "description": {  
                    "type": "string"  
                  },  
                  "type": {  
                    "enum": [  
                      "provider"  
                    ]  
                  },  
                  "connectionString": {  
                    "type": "string"  
                  },  
                  "impersonationMode": {  
                    "enum": [  
                      "default",  
                      "impersonateAccount",  
                      "impersonateAnonymous",  
                      "impersonateCurrentUser",  
                      "impersonateServiceAccount",  
                      "impersonateUnattendedAccount"  
                    ]  
                  },  
                  "account": {  
                    "type": "string"  
                  },  
                  "password": {  
                    "type": "string"  
                  },  
                  "maxConnections": {  
                    "type": "integer"  
                  },  
                  "isolation": {  
                    "enum": [  
                      "readCommitted",  
                      "snapshot"  
                    ]  
                  },  
                  "timeout": {  
                    "type": "integer"  
                  },  
                  "provider": {  
                    "type": "string"  
                  },  
                  "annotations": {  
                    "type": "array",  
                    "items": {  
                      "description": "Annotation object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "name": {  
                          "type": "string"  
                        },  
                        "value": {  
                          "anyOf": [  
                            {  
                              "type": "string"  
                            },  
                            {  
                              "type": "array",  
                              "items": {  
                                "type": "string"  
                              }  
                            }  
                          ]  
                        }  
                      },  
                      "additionalProperties": false  
                    }  
                  }  
                },  
                "additionalProperties": false  
              }  
            ]  
          }  
        },  
  
```  
  
## <a name="see-also"></a>请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
