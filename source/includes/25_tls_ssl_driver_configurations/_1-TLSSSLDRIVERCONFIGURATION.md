## TLS/SSL Driver Configuration

A “class” of connections that enable declaring secure (SSL) connections in a driver file (.c4i) is defined below. As part of this, the “port” section supports some additional properties that enable various features of SSL. Here is an example taken from the HC-800 driver file.
 
          `<classname>SSL</classname>`
          `<ports>`
            `<port>`
              `<name>Sysman</name>`
              `<number>5810</number>`
              `<auto_connect>True</auto_connect>`
              `<monitor_connection>True</monitor_connection>`
              `<keep_connection>True</keep_connection>`
              `<keep_alive>True</keep_alive>`
              `<delimiter>4f4b0a</delimiter>`
            `</port>`
        `  </ports>`
 
This snipped declares an SSL connection bound to port 5810 (Sysman). This particular connection doesn't require the use of any special properties. Here is another example that illustrates the five new properties that were added for SSL.
 
            `<port>`
              `<name>CertTest</name>`
              `<number>6666</number>`
              `<auto_connect>True</auto_connect>`
              `<monitor_connection>True</monitor_connection>`
              `<keep_connection>True</keep_connection>`
              `<keep_alive>True</keep_alive>`
              `<delimiter>4f4b0a</delimiter>`
             ` <certificate>./protected.pem</certificate>`
              `<private_key protected="True">./protected.pem</private_key>`
             `<cacert>./cacert.pem</cacert>`
             ` <verify_mode>peer</verify_mode>`
             ` <method>sslv3</method>`
           ` </port>`
 
The properties are defined as:
`certificate` - Path to the certificate to use for the connection. The path is relative to driver’s C4Z location.

`private**_key`- Path to the private key to use for the connection. The path is relative to the driver’s C4Z location. If the “protected” attribute is “True”, then Director will invoke the following callback to retrieve the password from the driver:

`function GetPrivateKeyPssword(Binding, Port)`
     ` return “TheKey”`
`end`

See below for GetPrivateKeyPassword definition.

`cacert` - Path to the CA (certificate authority) certificate to use for the connection. The path is relative to the driver’s C4Z location.

`verify_mode` - Specifies the verification mode to use for the connection. The verify mode corresponds to those supported by OpenSSL. A detailed description of the verification modes can be found here:

 `https://www.openssl.org/docs/ssl/SSL_CTX_set_verify.html. `_ 
Note that Control4 currently supports only the peer verification mode (`SSL_VERIFY_PEER`). Value values include:

- `none`
- `peer`

If this property is omitted, then Director defaults to use no verification (“none”).

`method` - Specifies the method to use for establishing the connection. A detailed description of the various methods can be found here: `https://www.openssl.org/docs/ssl/SSL_CTX_new.html`. Valid values include:

- `sslv2`
- `sslv23`
- `sslv3`
- `tlsv1`
- `tlsv1_1`

If this property is omitted, then Director defaults to using sslv23 (which is the OpenSSL default).


Please note that the `<certificate>`, `<private_key>`, and `<cacert>` expected in those XML tags for certificates and key information may all be contained in the same file.  It's not required to split the various certificates and keys out into separate files to work properly.  In the case that they are all contained in a single file, put that file's filename value in each of the XML tags.


## GetPrivateKeyPassword
This callback API supports password protection for SSL Certificates that are embedded within a device driver. Implementing GetPrivateKeyPassword within a .C4i file permits a password to be returned for a binding which requires an SSL Certificate. When implemented correctly, this API will return the string value of the SSL Certificate password. Use of this API is recommended in conjunction with encrypted drivers.
 
| Parameters | Description |
| — | — |
| num | idBinding: Binding ID of the network connection with the password-protected certificate. |
| num | nPort: Port number for the network connection with the password-protected certificate. |


|Returns | Value |
| — | — |
| str | strPassword: String value of the SSL Certificate password |