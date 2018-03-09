- Error Handling
  * DefaultResponseErrorHandler

- Enable debugging
  * logging.level.org.springframework.web.client=DEBUG

- MapStruct

- HttpComponentsClientHttpRequestFactory
  * connection timeout: the timeout in making the initial connection; i.e. completing the TCP connection handshake
  * read timeout: the timeout on waiting to read data. Specifically, if the server fails to send a byte <timeout> seconds after the last byte, a read timeout error will be raised.
    ```java
    HttpComponentsClientHttpRequestFactory requestFactory = new HttpComponentsClientHttpRequestFactory();
    requestFactory.setConnectTimeout(prop.getConnectTimeoutMS());
    requestFactory.setReadTimeout(prop.getReadTimeoutMS());

    RestTemplate restTemplate = new RestTemplate(requestFactory);
    ```
