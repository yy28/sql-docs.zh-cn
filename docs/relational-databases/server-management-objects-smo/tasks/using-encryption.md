---
title: 使用加密 |Microsoft 文档
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- database master key [SMO]
- cryptography [SMO]
- cryptography [SQL Server], SMO
- encryption keys [SMO]
- encryption [SQL Server], SMO
- encryption [SMO]
- certificates [SMO]
- service master key [SMO]
ms.assetid: 405e0ed7-50a9-430e-a343-471f54b4af76
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73c3a4a6ac3a433833e13fc45f67c1c5b509ef5d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-encryption"></a>使用加密
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 SMO 中，由服务主密钥<xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey>对象。 这由引用<xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A>属性<xref:Microsoft.SqlServer.Management.Smo.Server>对象。 它可以通过重新生成<xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A>方法。  
  
 数据库主密钥由<xref:Microsoft.SqlServer.Management.Smo.MasterKey>对象。 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A>属性指示是否通过服务主密钥加密数据库主密钥。 数据库主密钥发生变化时，主数据库中的加密副本会自动进行更新。  
  
 可以删除服务密钥加密使用<xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A>方法和使用密码加密数据库主密钥。 在这种情况下，您必须显式打开数据库主密钥，然后才能访问已受到安全保护的私钥。  
  
 当正在数据库附加到的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，必须提供数据库主密钥的密码，或执行<xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A>方法来执行数据库主密钥的未加密的副本可用于与服务的加密主密钥。 建议执行此步骤，从而无需显式打开数据库主密钥。  
  
 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A>方法重新生成数据库主密钥。 当重新生成数据库主密钥时，会对所有使用该数据库主密钥加密的密钥进行解密，然后使用新的数据库主密钥对其进行加密。 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A>方法会删除通过服务主密钥的数据库主密钥加密。 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> 可以通过服务主密钥对主密钥的副本进行加密，然后将副本存储在当前数据库和主数据库中。  
  
 在 SMO 中，证书由表示<xref:Microsoft.SqlServer.Management.Smo.Certificate>对象。 <xref:Microsoft.SqlServer.Management.Smo.Certificate>对象具有指定的公钥、 使用者名称、 有效期以及有关颁发者信息的段的属性。 可采用 **Grant**、 **Revoke** 和 **Deny** 方法控制对证书的访问权限。  
  
## <a name="example"></a>示例  
 对于下列代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。 有关详细信息，请参阅[创建 Visual C&#35; Visual Studio.NET 中的 SMO 项目](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="adding-a-certificate-in-visual-c"></a>在 Visual C# 中添加证书  
 该代码示例使用加密密码创建简单证书。 与其他对象不同<xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A>方法有多个重载。 该示例中所使用的重载将使用加密密码创建一个新证书。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            {  
                Server srv = new Server();  
  
                //Reference the AdventureWorks2012 database.   
                Database db = srv.Databases["AdventureWorks2012"];  
  
                //Define a Certificate object variable by supplying the parent database and name in the constructor.   
                Certificate c = new Certificate(db, "Test_Certificate");  
  
                //Set the start date, expiry date, and description.   
                System.DateTime dt;  
                DateTime.TryParse("January 01, 2010", out dt);  
                c.StartDate = dt;  
                DateTime.TryParse("January 01, 2015", out dt);  
                c.ExpirationDate = dt;  
                c.Subject = "This is a test certificate.";  
                //Create the certificate on the instance of SQL Server by supplying the certificate password argument.   
                c.Create("pGFD4bb925DGvbd2439587y");  
            }  
        }   
```  
  
## <a name="adding-a-certificate-in-powershell"></a>在 PowerShell 中添加证书  
 该代码示例使用加密密码创建简单证书。 与其他对象不同<xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A>方法有多个重载。 该示例中所使用的重载将使用加密密码创建一个新证书。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
#Create a certificate  
  
$c = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Certificate -argumentlist $db, "Test_Certificate"  
$c.StartDate = "January 01, 2010"  
$c.Subject = "This is a test certificate."  
$c.ExpirationDate = "January 01, 2015"  
  
#Create the certificate on the instance of SQL Server by supplying the certificate password argument.  
$c.Create("pGFD4bb925DGvbd2439587y")  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用加密密钥](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)  
  
  
