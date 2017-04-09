```
  gzip                          on;
  gzip_disable                  "MSIE [1-6]\.(?!.*SV1)";
  gzip_buffers                  16 8k;
  gzip_comp_level               6;
  gzip_http_version             1.1;
  gzip_min_length               10;
  gzip_types                    text/plain text/css application/x-javascript text/xml application/xml application/xml+rss text/javascript;
  gzip_vary                     on;
  gzip_proxied                  any; # Compression for all requests.
```