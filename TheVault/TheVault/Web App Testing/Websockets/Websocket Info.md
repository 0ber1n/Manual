- The `Connection` and `Upgrade` headers in the request and response indicate that this is a WebSocket handshake.
- The `Sec-WebSocket-Version` request header specifies the WebSocket protocol version that the client wishes to use. This is typically `13`.
- The `Sec-WebSocket-Key` request header contains a Base64-encoded random value, which should be randomly generated in each handshake request.
- The `Sec-WebSocket-Accept` response header contains a hash of the value submitted in the `Sec-WebSocket-Key` request header, concatenated with a specific string defined in the protocol specification. This is done to prevent misleading responses resulting from misconfigured servers or caching proxies.

