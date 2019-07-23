---
title: JDBC 中的 FIPS 模式 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
manager: kenvh
ms.openlocfilehash: 482e820d17860b67f46d47f4bb8523e833d0cf5a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68252216"
---
# <a name="fips-mode"></a>FIPS 模式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

适用于 SQL Server 的 Microsoft JDBC Driver 支持在配置为*符合 FIPS 140*的 jvm 中运行。

#### <a name="prerequisites"></a>必备条件

- FIPS 配置 JVM
- 适当的 SSL 证书
- 适当的策略文件
- 适当的配置参数

## <a name="fips-configured-jvm"></a>FIPS 配置 JVM

通常, 应用程序可以将`java.security`该文件配置为使用符合 FIPS 标准的加密提供程序。 有关如何配置 FIPS 140 符合性的详细说明, 请参阅特定于 JVM 的文档。

若要查看已批准的 FIPS 配置模块, 请参阅[加密模块验证计划中的已验证模块](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules)。

供应商可能会执行一些额外的步骤来配置具有 FIPS 的 JVM。

## <a name="appropriate-ssl-certificate"></a>适当的 SSL 证书
为了连接到 FIPS 模式下的 SQL Server, 需要一个有效的 SSL 证书。 将其安装或导入到启用 FIPS 的客户端计算机 (JVM) 上的 Java 密钥存储中。

### <a name="importing-ssl-certificate-in-java-keystore"></a>在 Java 密钥库中导入 SSL 证书
对于 FIPS, 很可能需要以 PKCS 或特定于提供程序的格式导入证书 (证书)。
使用以下代码片段导入 SSL 证书, 并将其存储在具有适当的密钥存储格式的工作目录中。 _信任\_存储区\_密码_是 Java 密钥库的密码。

```java
public void saveGenericKeyStore(
        String provider,
        String trustStoreType,
        String certName,
        String certPath
        ) throws KeyStoreException, CertificateException,
            NoSuchAlgorithmException, NoSuchProviderException,
            IOException
{
    KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
    FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
    ks.load(null, null);
    ks.setCertificateEntry(certName, getCertificate(certPath));
    ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
    os.flush();
    os.close();
}

private Certificate getCertificate(String pathName)
        throws FileNotFoundException, CertificateException
{
    FileInputStream fis = new FileInputStream(pathName);
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    return cf.generateCertificate(fis);
}
```

下面的示例使用 BouncyCastle 提供程序导入 PKCS12 格式的 Azure SSL 证书。 使用以下代码片段, 将证书导入名为_MyTrustStore\_PKCS12_的工作目录中:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>适当的策略文件
对于某些 FIPS 提供程序, 需要无限制的策略 jar。 在这种情况下, 对于 Sun/Oracle, 请为[JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)或[Jre 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)下载 JAVA 加密扩展 (JCE) 不受限制的区域策略文件。 

## <a name="appropriate-configuration-parameters"></a>适当的配置参数
若要在符合 FIPS 的模式下运行 JDBC 驱动程序, 请按下表中所示配置连接属性。 

#### <a name="properties"></a>属性 

|属性|类型|，则“默认”|描述|说明|
|---|---|---|---|---|
|encrypt|布尔 [“true / false”]|“false”|对于启用 FIPS 的 JVM 加密属性应为**true**||
|TrustServerCertificate|布尔 [“true / false”]|“false”|对于 FIPS, 用户需要验证证书链, 因此用户应使用此属性的 **"false"** 值。 ||
|trustStore|String|null|你在其中导入证书的 Java 密钥库文件路径。 如果在系统上安装证书, 则无需传递任何内容。 驱动程序使用 cacerts 或 j 文件。||
|trustStorePassword|String|null|用于检查 trustStore 数据完整性的密码。||
|fips|布尔 [“true / false”]|“false”|对于启用 FIPS 的 JVM, 此属性应为**true**|添加在6.1.4 中 (稳定版本 6.2.2)||
|fipsProvider|String|null|JVM 中配置的 FIPS 提供程序。 例如, BCFIPS 或 SunPKCS11 |添加在6.1.2 中 (稳定版本 6.2.2), 已在 v6.4.0 中弃用-请在[此处](https://github.com/Microsoft/mssql-jdbc/pull/460)查看详细信息。|
|trustStoreType|String|JKS|对于 FIPS 模式, 请将信任存储类型设置为 PKCS12 或由 FIPS 提供程序定义的类型。 |添加在6.1.2 中 (稳定版本 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
