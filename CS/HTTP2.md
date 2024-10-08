# HTTP/1과 HTTP/2 비교

1. 성능
   HTTP/1: 각 요청마다 별도의 TCP 연결을 사용합니다. 이를 **"헤드 오브 라인 블로킹(Head-of-Line Blocking)"**이라고 하며, 하나의 요청이 완료될 때까지 다른 요청이 대기해야 하는 상황이 발생할 수 있습니다. 이를 해결하기 위해, 클라이언트는 여러 연결을 열어 요청을 병렬로 보내지만, 이는 네트워크 자원을 비효율적으로 사용하게 만듭니다.

HTTP/2: 멀티플렉싱(Multiplexing) 기능을 도입하여, 하나의 TCP 연결에서 여러 요청을 동시에 처리할 수 있습니다. 즉, 요청들이 순차적으로 처리되지 않고 동시에 전송되고, 응답도 병렬로 받을 수 있어 성능이 크게 향상됩니다.

2. 헤더 압축
   HTTP/1: 요청과 응답마다 헤더가 함께 전송되며, 이 헤더는 반복적인 정보가 많아 데이터를 많이 차지합니다.

HTTP/2: HPACK이라는 헤더 압축 방식을 사용해 헤더의 중복을 줄이고, 전체 데이터 전송량을 줄입니다. 이를 통해 성능이 더욱 향상됩니다.

3. 서버 푸시(Server Push)
   HTTP/1: 클라이언트가 요청한 리소스만 전송합니다. 클라이언트가 다른 리소스를 요청하기 전까지 기다려야 합니다.

HTTP/2: 서버가 클라이언트가 필요할 것으로 예상되는 리소스를 미리 전송할 수 있는 서버 푸시 기능을 지원합니다. 이를 통해 페이지 로드 속도를 더 빠르게 할 수 있습니다.

4. 연결 유지
   HTTP/1: 클라이언트와 서버 간의 연결을 유지하려면 주기적으로 "Keep-Alive" 요청을 보내야 합니다. 또한, HTTP/1.1에서는 Keep-Alive가 기본으로 활성화되어 있지만, 여전히 각 요청마다 새로운 연결을 여는 경우가 많습니다.

HTTP/2: 기본적으로 하나의 연결을 통해 모든 요청을 처리하며, 연결 유지에 대한 추가적인 설정 없이도 효율적으로 작동합니다.

5. 보안
   HTTP/1: HTTP/1.1에서는 보안이 별도의 SSL/TLS 계층에서 처리되며, 암호화는 선택 사항입니다.

HTTP/2: HTTP/2는 HTTPS(암호화된 HTTP) 위에서만 작동하도록 요구하는 경우가 많으며, 보안이 기본적으로 강화되었습니다.

이와 같이, HTTP/2는 HTTP/1에 비해 더 빠르고 효율적인 데이터 전송을 가능하게 하며, 현대 웹 애플리케이션의 성능을 크게 향상시키는 데 중요한 역할을 합니다.

## 참고

- [더 빠른 웹을 위한 더 나은 HTTP/2 우선순위 지정](https://blog.cloudflare.com/better-http-2-prioritization-for-a-faster-web/)
