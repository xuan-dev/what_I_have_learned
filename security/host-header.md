Reference: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Forwarded-Host

A successful host header injection could result in web cache poisoning, password reset poisoning, access to internal hosts, cross-site scripting (XSS), bypassing authentication, virtual host brute-forcing, redirecting.

### RECOMMENDATION
Avoid using the Host header altogether in server-side code. Double-check whether each URL really needs to be absolute. You will often find that you can just use a relative URL instead. This simple change can help you prevent web cache poisoning vulnerabilities in particular.


        
      Validate the Host header

        
      Don't support Host override headers

        
      Whitelist permitted domains
