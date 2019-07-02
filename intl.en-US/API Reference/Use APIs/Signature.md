# Signature {#concept_vr2_brn_12b .concept}

RDS performs authentication on each access request. Therefore, each request, whether being sent by HTTP or HTTPS, must contain signature information. RDS performs symmetric encryption using the ‘Access Key ID’ and ‘Access Key Secret’ to authenticate the request sender. The Access Key ID and Access Key Secret are officially issued to visitors by Alibaba Cloud \(visitors can apply for and manage them at Alibaba Cloud’s official website\). The Access Key ID indicates the identity of the visitor. The Access Key Secret is the secret key used to encrypt and verify the signature string on the server. It must be kept confidential and only be available to Alibaba Cloud and you.

When you call a server, the following method is used to sign the request:

1.  Construct a normalized request string \(Canonicalized Query String\) using request parameters.
    1.  Request parameters are ordered alphabetically by their names \(including public request parameters and user-defined parameters for the given request interfaces described in this document, but excluding the Signature parameter mentioned in public request parameters\).

        **Note:** For a request submitted using the GET method, these parameters constitute the parameter section of the request URL \(that is, the section in the URL following “?” and connected by “&”\).

    2.  The name and value of each request parameter are encoded. The names and values must be URL-encoded using the UTF-8 character set. The URL encoding rules are as follows:
        1.  The characters A-Z, a-z, 0-9, and “-“, “\_”, “.”, “~” are not encoded.
        2.  Other characters are encoded in “%XY” format, with XY representing the characters’ ASCII code in hexadecimal notation. For example, the English double quotes \(“\) are encoded as %22.
        3.  Extended UTF-8 characters are encoded in “%XY%ZA…” format.
        4.  It must be noted that an English space is encoded as %20, rather than the plus sign \(+\).

            **Note:** Generally, libraries that support URL encoding \(such as Java’s java.net.URLEncoder\) encode characters according to the rules for the MIME-type “application/x-www-form-urlencoded”. If this encoding method is used, replace the plus signs \(+\) in the encoded strings with %20, the asterisks \(\*\) with %2A, and change %7E back to the tilde \(~\) to conform to the preceding encoding rules.

    3.  Connect the encoded parameter names and values with the equal sign \(=\).
    4.  Sort the parameter name and value pairs connected by equal signs in alphabetical order, and connect them with the \(&\) symbol to produce the Canonicalized Query String.
2.  Follow the following rules to construct the string used for signature calculation by using the Canonicalized Query String constructed in the previous step:

    ``` {#codeblock_412_dvw_awj}
    StringToSign=
    HTTPMethod + "&" +
    percentEncode("/") + "&" +
    percentEncode(CanonicalizedQueryString)
    ```

    Parameter description:

    -   HTTPMethod: the HTTP method used for request submission, for example, GET.
    -   percentEncode\(“/“\): the coded value for the character “/“ according to the URL encoding rules described in 1.b, namely, “%2F”.
    -   percentEncode\(CanonicalizedQueryString\): the encoded string of the Canonicalized Query String constructed in Step 1, produced by following the URL encoding rules described in 1.b.
3.  Use the preceding signature sting to calculate the signature’s HMAC value based on RFC2104 definitions.

    **Note:** The Key used for calculating the signature is the Access Key Secret held by you, which ends with the “&” character \(ASCII:38\) and is based on the SHA1 hashing.

4.  According to Base64 encoding rules, encode the preceding HMAC value into a string, which gives you the signature value.
5.  Add the obtained signature value to the request parameters as the Signature parameter, which completes the request signing process.

    **Note:** 

    When the obtained signature value is submitted to the RDS server as the final request parameter value, the value is URL-encoded like other parameters according to RFC3986 rules.

    DescribeDBInstances is used as an example. The request URL before signature is as follows:

    ``` {#codeblock_q90_zlb_d1h}
    http://rds.aliyuncs.com/?Timestamp=2013-06-01T10:33:56Z&Format=XML&AccessKeyId=testid&Action=DescribeDBInstances&SignatureMethod=HMAC-SHA1&RegionId=region1&SignatureNonce=NwDAxvLU6tFE0DVb&Version=2014-08-15&SignatureVersion=1.0
    ```

    Thus, the StringToSign is:

    ``` {#codeblock_5tz_7sl_whu}
    GET&%2F&AccessKeyId%3Dtestid&Action%3DDescribeDBInstances&Format%3DXML&RegionId%3Dregion1&SignatureMethod%3DHMAC-SHA1&SignatureNonce%3DNwDAxvLU6tFE0DVb&SignatureVersion%3D1.0&Timestamp%3D2013-06-01T10%253A33%253A56Z&Version%3D2014-08-15
    ```

    Assume that the Access Key ID is testid, the Access Key Secret is testsecret, and the Key used for HMAC calculation is testsecret&. The calculated signature is: `cNr+cHw3awqsBaWs6J6hcGvnfJE=` 

    The signed request URL is \(added with the Signature parameter\):

    ``` {#codeblock_i3l_m15_3gb}
    http://rds.aliyuncs.com/?Timestamp=2013-06-01T10%3A33%3A56Z&Format=XML&AccessKeyId=testid&Action=DescribeDBInstances&SignatureMethod=HMAC-SHA1&RegionId=region1&SignatureNonce=NwDAxvLU6tFE0DVb&SignatureVersion=1.0&Version=2014-08-15&Signature=cNr%2bcHw3awqsBaWs6J6hcGvnfJE%3d
    ```


