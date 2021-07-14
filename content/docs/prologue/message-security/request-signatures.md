---
title: "Request Signatures"
slug: "request-signatures"
hidden: false
createdAt: "2018-09-02T12:37:41.671Z"
updatedAt: "2021-07-01T08:10:21.337Z"
---
When you send an HTTPS REST request to the Rapyd Payments platform, you must include specified header parameters, including a signature. These headers are required for both the production platform and the sandbox. The headers are not required in the response from your remote authorization server.

The signing process helps secure requests in the following ways:

* Verifies that the requester is an authorized user. 
* Protects data from tampering in transit.
* Rejects requests from unauthorized persons.

When you send a request, you calculate the signature and insert the result into the `signature` header. When the platform receives the request, it performs the same signature calculation. If the resulting values do not match, the request is rejected.
[block:api-header]
{
  "title": "Calculation of Signature"
}
[/block]
The signature is calculated as a hash of a concatenation of specific strings, according to the following formula:

 ** *signature* = BASE64 ( HASH ( *http_method* + *url_path* + *salt* + *timestamp* + *access_key* + *secret_key* + *body_string* ) )**

where:
* ***BASE64*** is a Base-64 encoding algorithm.
* ***HASH*** is the HMAC-SHA256 algorithm.
* ***http_method*** is the HTTP method, in lower-case letters. Relevant to version 1.0.3 and forward.
* ***url_path*** is the portion of the URL after the base URI, such as **https://api.rapyd.net**. The URL path starts with **/v1**. Relevant to version 1.0.3 and forward.
* ***salt*** is a random numeric string for each request. Length: 8-16 digits.
* ***timestamp*** is the time of the request, in [*Unix time*](ref:glossary). The Rapyd platform is synchronized to the actual current time, as defined by public NTP servers. See [*NTP*](ref:glossary). The timestamp must be synchronized to the actual current time, or less than 60 seconds before the actual current time.
* ***access_key*** is a unique string for each user, assigned by Rapyd.
* ***secret_key*** is a unique string for each user, assigned by Rapyd. The secret key is like a password, and is transmitted only as part of the calculated signature. Do not share it with your customers or partners, and do not transmit it in plaintext.
* ***body_string*** is a valid JSON string (relevant to requests that contain a body). If the body is empty, it must be empty in the request and in the signature calculation, and not empty curly braces {}.
[block:callout]
{
  "type": "warning",
  "title": "Note",
  "body": "Different languages handle Base-64 encoding differently. You must adequately test your code so that all messages are encoded with all the correct Base-64 options."
}
[/block]

[block:api-header]
{
  "title": "Code Examples"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "import org.apache.http.HttpEntity;\nimport org.apache.http.HttpResponse;\nimport org.apache.http.client.ClientProtocolException;\nimport org.apache.http.client.HttpClient;\nimport org.apache.http.client.ResponseHandler;\nimport org.apache.http.client.methods.HttpGet;\nimport org.apache.http.impl.client.HttpClients;\nimport org.apache.http.util.EntityUtils;\n\nimport javax.crypto.Mac;\nimport javax.crypto.spec.SecretKeySpec;\nimport java.io.IOException;\nimport java.io.UnsupportedEncodingException;\nimport java.security.InvalidKeyException;\nimport java.security.MessageDigest;\nimport java.security.NoSuchAlgorithmException;\nimport java.util.Base64;\nimport java.util.Random;\n\npublic class GetPOS {\n    \n    public static String hash256(String data) throws NoSuchAlgorithmException {\n        MessageDigest md = MessageDigest.getInstance(\"SHA-256\");\n        md.update(data.getBytes());\n        return bytesToHex(md.digest());\n    }\n    \n    public static String bytesToHex(byte[]bytes) {\n        StringBuffer result = new StringBuffer();\n        for (byte byt: bytes)\n            result.append(Integer.toString((byt & 0xff) + 0x100, 16).substring(1));\n        return result.toString();\n    }\n    \n    public static String hmacDigest(String msg, String keyString, String algo) {\n        String digest = null;\n        try {\n            SecretKeySpec key = new SecretKeySpec((keyString).getBytes(\"ASCII\"), algo);\n            Mac mac = Mac.getInstance(algo);\n            mac.init(key);\n            \n            byte[]bytes = mac.doFinal(msg.getBytes(\"ASCII\"));\n            \n            StringBuffer hash = new StringBuffer();\n            for (int i = 0; i < bytes.length; i++) {\n                String hex = Integer.toHexString(0xFF & bytes[i]);\n                if (hex.length() == 1) {\n                    hash.append('0');\n                }\n                hash.append(hex);\n            }\n            digest = hash.toString();\n        } catch (UnsupportedEncodingException e) {\n            System.out.println(\"hmacDigest UnsupportedEncodingException\");\n        }\n        catch (InvalidKeyException e) {\n            System.out.println(\"hmacDigest InvalidKeyException\");\n        }\n        catch (NoSuchAlgorithmException e) {\n            System.out.println(\"hmacDigest NoSuchAlgorithmException\");\n        }\n        return digest;\n    }\n    \n    public static String givenUsingPlainJava_whenGeneratingRandomStringUnbounded_thenCorrect() {\n        int leftLimit = 97;   // letter 'a'\n        int rightLimit = 122; // letter 'z'\n        int targetStringLength = 10;\n        Random random = new Random();\n        StringBuilder buffer = new StringBuilder(targetStringLength);\n        for (int i = 0; i < targetStringLength; i++) {\n            int randomLimitedInt = leftLimit + (int)\n                (random.nextFloat() * (rightLimit - leftLimit + 1));\n            buffer.append((char)randomLimitedInt);\n        }\n        String generatedString = buffer.toString();\n        \n        return (generatedString);\n    }\n\n    public static void main(String[]args)throws Exception {\n        try {\n            System.out.println(\"GetPOS Start\");\n            String salt = givenUsingPlainJava_whenGeneratingRandomStringUnbounded_thenCorrect(); // Randomly generated for each request.\n            long timestamp = System.currentTimeMillis() / 1000L; // Unix time.\n            String accessKey = \"AAAAAAAAAAA\";                    // The access key received from Rapyd.\n            String secretKey = \"SSSSSSSSSSS\";                    // Never transmit the secret key by itself.\n            String toEnc = \"get/v1/data/countries\" + salt + Long.toString(timestamp) + accessKey + secretKey;\n            System.out.println(\"String TO BE Encrypted::\" + toEnc);\n            String StrhashCode = hmacDigest(\"get/v1/data/countries\" + salt +\n                    Long.toString(timestamp) +\n                    accessKey +\n                    secretKey, \"HmacSHA256\");\n            String signature = Base64.getEncoder().encodeToString(StrhashCode.getBytes());\n            HttpClient httpclient = HttpClients.createDefault();\n            \n            try {\n                HttpGet httpget = new HttpGet(\"https://sandboxapi.rapyd.net/v1/data/countries\");\n                \n                httpget.addHeader(\"Content-Type\", \"application/json\");\n                httpget.addHeader(\"access_key\", accessKey);\n                httpget.addHeader(\"salt\", salt);\n                httpget.addHeader(\"timestamp\", Long.toString(timestamp));\n                httpget.addHeader(\"signature\", signature);\n                \n                // Create a custom response handler\n                ResponseHandler < String > responseHandler = new ResponseHandler < String > () {\n                     @ Override\n                    public String handleResponse(\n                        final HttpResponse response)throws ClientProtocolException,\n                    IOException {\n                        int status = response.getStatusLine().getStatusCode();\n                        HttpEntity entity = response.getEntity();\n                        return entity != null ? EntityUtils.toString(entity) : null;\n                    }\n                };\n                String responseBody = httpclient.execute(httpget, responseHandler);\n                System.out.println(\"----------------------------------------\");\n                System.out.println(responseBody);\n            }\n            finally {\n            }\n        } catch (Exception e) {\n        }\n    }\n}\n",
      "language": "java",
      "name": "Java"
    },
    {
      "code": "// Note: Install the crypto-js module.\n\nvar http_method = 'get';                // Lower case.\nvar url_path = '/v1/data/countries';    // Portion after the base URL.\nvar salt = CryptoJS.lib.WordArray.random(12);  // Randomly generated for each request.\nvar timestamp = (Math.floor(new Date().getTime() / 1000) - 10).toString();\n                                        // Current Unix time.\nvar access_key = 'your-access-key';     // The access key received from Rapyd.\nvar secret_key = 'your-secret-key';     // Never transmit the secret key by itself.\nvar body = '';                          // JSON body goes here.\n\nif (JSON.stringify(request.data) !== '{}' && request.data !== '') {\n\tbody = JSON.stringify(JSON.parse(request.data));\n}\n\nvar to_sign = http_method + url_path + salt + timestamp + access_key + secret_key + body;\n\nvar signature = CryptoJS.enc.Hex.stringify(CryptoJS.HmacSHA256(to_sign, secret_key));\n\nsignature = CryptoJS.enc.Base64.stringify(CryptoJS.enc.Utf8.parse(signature));",
      "language": "javascript",
      "name": "NODE.js"
    },
    {
      "code": "// This example shows how you might transmit the headers, including the signature. You must calculate the signature before the curl call.\n\ncurl -X GET https://sandboxapi.rapyd.net/v1/data/countries\n     -H \"Content-Type: application/json\"\n     -H \"salt: random-number\"\n     -H \"timestamp: current-unix-time\"\n     -H \"access_key: your-access-key\"\n     -H \"signature: your-calculated-signature\"\n     -d \"request_body_goes_here\"",
      "language": "text",
      "name": "cURL"
    },
    {
      "code": "require 'digest'\nrequire 'base64'\nrequire 'json'\nrequire 'uri'\nrequire 'net/http'\nrequire 'OpenSSL'\n\no = [('a'..'z')].map( & : to_a).flatten\nSALT = ((0...8).map { o[rand(o.length)] }.join # Randomly generated for each request.\n\nTIMESTAMP = Time.now.to_i.to_s      # Current Unix time.\n\nputs SALT\nputs TIMESTAMP\n\nSECRET_KEY = 'your-secret-key'      # Never transmit the secret key by itself.\nACCESS_KEY = 'your-access-key'      # The access key received from Rapyd.\nREL_PATH = 'get/v1/data/countries'  # HTTP method plus the portion after the base URL.\n\ndef signature body\n  to_sign = \"#{REL_PATH}#{SALT}#{TIMESTAMP}#{ACCESS_KEY}#{SECRET_KEY}\"\n  puts to_sign\n  mac = OpenSSL::HMAC.hexdigest(\"SHA256\", \"your-secret-key\", to_sign)\n  puts mac\n  temp_BS64 = Base64.urlsafe_encode64(mac)\n  puts temp_BS64\n  temp_BS64\nend\n\ndef set_headers request, body\n  puts signature(body)\n  request['content-type'] = 'application/json'\n  request['signature'] = signature(body)\n  request['salt'] = SALT\n  request['timestamp'] = TIMESTAMP\n  request['access_key'] = ACCESS_KEY\n  request\nend\n\ndef getFromRapyd(body, url)\n  uri = URI(url)\n  res = Net::HTTP.start(uri.host, uri.port, use_ssl: true) do |http|\n    request = Net::HTTP::Get.new(uri)\n    set_headers request, body\n    http.request(request)\n  end\n\n  puts res.read_body\nend\n\ndef getCountries\n  body = ''\n  getFromRapyd(body, \"https://sandboxapi.rapyd.net/v1/data/countries\")\nend\n\ngetCountries\n",
      "language": "ruby",
      "name": "Ruby"
    },
    {
      "code": "import hashlib\nimport base64\nimport json\nimport requests\nfrom datetime import datetime\nimport calendar\nimport string\nfrom random import *\nimport hmac\n\nidempotency_key = 'aee984befae64'     # Unique for each 'Create Payment' request.\n\nhttp_method = 'get'                   # Lower case.\nbase_url = 'https://sandboxapi.rapyd.net'\npath = '/v1/data/countries' # Portion after the base URL.\n\n# salt: randomly generated for each request.\nmin_char = 8\nmax_char = 12\nallchar = string.ascii_letters + string.punctuation + string.digits\nsalt = \"\".join(choice(allchar)for x in range(randint(min_char, max_char)))\n\n# Current Unix time.\nd = datetime.utcnow()\ntimestamp = calendar.timegm(d.utctimetuple())\n\naccess_key = 'your-access-key'   # The access key received from Rapyd.\nsecret_key = 'your-secret-key'   # Never transmit the secret key by itself.\n\nbody = ''                        # JSON body goes here.\n\nto_sign = http_method + path + salt + str(timestamp) + access_key + secret_key + body\n\nh = hmac.new(bytes(secret_key, 'utf-8'), bytes(to_sign, 'utf-8'), hashlib.sha256)\n\nsignature = base64.urlsafe_b64encode(str.encode(h.hexdigest()))\n\nurl = base_url + path\n\nheaders = {\n\t'access_key': access_key,\n\t'signature': signature,\n\t'salt': salt,\n\t'timestamp': str(timestamp),\n\t'Content-Type': \"application\\/json\",\n\t'idempotency': idempotency_key\n}\n\nprint(url)\n\nr = requests.get(url, headers = headers)\nprint(r.text)\n",
      "language": "python",
      "name": "Python"
    },
    {
      "code": "<?php\n\n$idempotency = 'aee984befae64';      // Unique for each 'Create Payment' request.\n$http_method = 'get';                // Lower case.\n$path = '/v1/data/countries';        // Portion after the base URL.\n$salt = mt_rand(10000000, 99999999); // Randomly generated for each request.\n$date = new DateTime();\n$timestamp = $date->getTimestamp();  // Current Unix time.\n$access_key = 'your-access-key';     // The access key received from Rapyd.\n$secret_key = 'your-secret-key';     // Never transmit the secret key by itself.\n$body = array();                     // JSON body goes here.\n$body_string = json_encode($body);\n\n$sig_string = $http_method.$path.$salt.$timestamp.$access_key.$secret_key;\n\n$hash_sig_string = hash_hmac(\"sha256\", $sig_string, $secret_key);\n\n$signature = base64_encode($hash_sig_string);\n\n$curl = curl_init();\ncurl_setopt_array($curl, array(\n\tCURLOPT_URL => \"https://sandboxapi.rapyd.net/v1/data/countries\",\n\tCURLOPT_POST => false,\n\tCURLOPT_RETURNTRANSFER => true,\n\t// CURLOPT_POSTFIELDS => $body_string\n));\n\ncurl_setopt($curl, CURLOPT_HTTPHEADER, array(\n\t'Content-Type: application/json',\n\t'access_key: '.$access_key.'',\n\t'salt: '.$salt.'',\n\t'timestamp: '.$timestamp.'',\n\t'signature: '.$signature.'',\n\t'idempotency: '.$idempotency.'' \n));\n\n$response = curl_exec($curl);\n\n$err = curl_error($curl);\n\ncurl_close($curl);\n\nif ($err) {\n\techo \"cURL Error #:\".$err;\n\t} else {\n\techo $response;\n}\n\n?>\n",
      "language": "php"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Related Information"
}
[/block]
* [Webhook Signatures](ref:webhook-signatures) - Describes the formula for calculating a signature for webhooks.