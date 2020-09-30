# Create a fully encrypted database on an ApsaraDB RDS for PostgreSQL instance

This topic describes how to create a fully encrypted database on an ApsaraDB RDS for PostgreSQL instance. Data stored in this database is encrypted before it is uploaded from the user end. Therefore, RDS can defend against both internal and external security threats, and the cloud data is only accessible to specific users.

Fully encrypted RDS databases are developed solely by DAMO Academy. Only the data owners, such as the owners of RDS instances or applications, can view user data in plaintext. This prevents against data breach on the cloud.

Fully encrypted RDS databases provide a Trusted Execution Environment \(TEE\). This allows data to be encrypted when it is uploaded from the user end to an RDS database. This type of RDS database stores all data in ciphertext. When you perform common database operations, ciphertext ensures that cloud platform software and management personnel cannot view the data in plaintext. The software includes operating systems, Virtual Machine Manager \(VMM\), and privilege management tools. The management personnel include database administrators. The operations include transactions, queries, and analytics.

## Scenarios

Fully encrypted RDS databases provide powerful security protection while ensuring the high performance, high reliability, and cost-effectiveness of the database system. The databases are suited for scenarios where the confidentiality and integrity of sensitive data must be guaranteed. Typical scenarios are as follows:

-   Encrypting data to be transmitted from applications to databases

    In common scenarios, data owners refer to application providers. The providers want to prevent the database service and its O&M personnel from accessing application data. These providers also want to ensure that databases are running as expected.

-   Encrypting data to be transmitted from users to applications

    In user-oriented businesses, users own part of data such as health data and financial data. The users want to use the data management and analysis capabilities of applications. Also, these users want to prevent applications from accessing private user data in plaintext.

-   Sharing encrypted data in a secure and reliable manner

    When sharing data with a third party, data owners want to encrypt the data without leaking their keys.


## Create a fully encrypted RDS database

The fully encrypted RDS database function is still in invitational preview. Only the users who receive invitations from Alibaba Cloud can create this type of database. The creation procedure is as follows:

1.  Create an RDS instance with the instance type set to a value that contains **SGX**.

    **Note:** For more information about other parameters, see [Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md).

2.  [Use DMS to log on to the RDS instance and create a database](/intl.en-US/RDS PostgreSQL Database/Database/Create a database on an ApsaraDB RDS for PostgreSQL instance.md).

3.  Execute the following statement to load the security plug-in ENCDB for the created database:

    ```
    CREATE EXTENSION ENCDB;
    ```


## Use a fully encrypted RDS database

You can use SDKs to access a fully encrypted RDS database from your client. Perform the following operations:

1.  Define encrypted fields.

    Fully encrypted RDS databases support both encrypted and non-encrypted fields. You can determine the sensitive fields that need to be encrypted and replace the data types of the sensitive fields with the data types after encryption.

    For example, execute the following statement to create a user\_profile table:

    ```
    CREATE TABLE user_profile (
      id int,
      name varchar,
      dob date,
      department varchar,
      salary int,
      primary key (id)
    )
    ```

    If you determine the id, name, salary, and dob fields as sensitive fields, create a table to import and encrypt these fields. Execute the following statement to create the table:

    ```
    CREATE TABLE user_profile (
      id enc_int4,
      name enc_varchar,
      dob enc_date,
      department varchar,
      salary enc_int4,
      primary key (id)
    )
    ```

    The following table describes the mappings between the original data types and the data types after encryption.

    |Original data type|Data type after encryption|
    |------------------|--------------------------|
    |int|enc\_int4|
    |float|enc\_float4|
    |text|enc\_text|
    |timestamp|enc\_timestamp|
    |int8|enc\_int8|
    |float8|enc\_float8|

2.  Modify a statement to query ciphertext.

    If you want to query sensitive fields, convert the values of the sensitive fields from the original data types to the data types after encryption.

    Use the SALARY field as the query condition. The original query statement is as follows:

    ```
    String selectSQL = "SELECT ID,NAME FROM user_profile WHERE SALARY > ? and SALARY < ?" ;
    preparedStatement.set(1, 2000);
    preparedStatement.set(2, 5000);
    ```

    Modify the query statement as follows:

    ```
    String selectSQL = "SELECT ID,NAME FROM user_profile WHERE SALARY > ? and SALARY < ?" ;
    preparedStatement.set(1, sdk.encrypt(2000));
    preparedStatement.set(2, sdk.encrypt(5000));
    ```

3.  Parse ciphertext.

    The query results are in ciphertext and must be parsed to obtain the plaintext.

    The following example parses the query results of the ID and NAME fields in the encdb table:

    ```
    Int id = sdk.decrypt(result.get("ID"));
    String name = sdk.decrypt(result.get("NAME"));
    ```


The following example shows complete code on your client:

```
// Connect to a database.
Connection con = DriverManager.getConnection("jdbc:XXX", "user1", "user1");
// Initialize Crypto SDK and pass the root key to TEE through remote attestation.
Crypto sdk(con, ROOT_KEY);
String selectSQL = "SELECT ID,NAME FROM user_profile WHERE SALARY > ? and SALARY < ?
and DOB < ?" ;
PreparedStatement stat = con.prepareStatement(sql);
// Obtain the required encryptors to encrypt different fields.
Encryptor enc_id = sdk.GetEncryptorByName("USER_PROFILE", "ID");
Encryptor enc_dob = sdk.GetEncryptorByName("USER_PROFILE", "DOB");
preparedStatement.set(1, enc_id.encypt(2000));
preparedStatement.set(2, enc_id.encypt(5000));
preparedStatement.set(3, enc_dob.encypt("1990-01-01"));
ResultSet rs = preparedStatement.executeQuery(selectSQL);
// Obtain the required decryptor to decrypt the query results.
Decryptor dec = sdk.GetDecryptor();
for (Result& r : rs) {
  // dec automatically obtains the data keys for the ID and NAME fields.
  Int id = dec.decrypt(r.get("ID"));
  String name = dec.decrypt(r.get("NAME"));
}
```

**Note:**

-   You must provide the correct root key to initialize the SDK.
-   Different fields can be encrypted by using different encryptors.
-   All query results are decrypted by using the same decryptor.

## Use SDK in applications

Follow these steps to use SDK. For more information, see README.md.

**Note:** [Click here to download the client SDK package that is supported by fully encrypted RDS databases](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/144151/cn_zh/1574652114855/encdbsdk.tar.gz).

-   Only the client SDK of x86\_64 is provided. It has been tested on Linux.
-   The client SDK provides complete C++ sample code. Compile the code and test it by referring to the example.cpp file.
-   The client SDK provides complete API descriptions. For more information, see the API.md file.

1.  Decompress the SDK package to the target path. Example: path/to/encdbsdk/.
2.  Call the SDK API in program code. Only the crypto.h file is required. Example:

    ```
    #include "crypto.h"
    ```

3.  Add the SDK to the compilation parameters and compile the program. The Makefile file is used. Example:

    ```
    CFLAGS += -I<path/to/encdbsdk>/include
    LDFLAGS += -L<path/to/encdbsdk>/lib64 -lencdb
    ```

4.  Run the program.

    **Note:** Make sure that <path/to/encdbsdk\>/lib64 can be found because the SDK is linked as a dynamic library. Run the following shell command to configure that path:

    ```
    export LD_LIBRARY_PATH=<path/to/encdbsdk>/lib64:$LD_LIBRARY_PATH
    ```


## Effects

-   Servers and unauthorized users can view sensitive data only in ciphertext, as shown in the following figure.

    ![Encryption effect](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7450359951/p67977.png)

-   Authorized users have the root keys and can decrypt the ciphertext by using the root keys to view sensitive data in plaintext.

    **Note:** The **Plain value** column shows the plaintext data that is generated after the data in the Cipher column is decrypted.

    ![Decryption effect](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7450359951/p67978.png)


