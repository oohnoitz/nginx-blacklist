# Nginx Bad Bot Blocker
**This was inspired by [bluedragonz/bad-bot-blocker](https://github.com/bluedragonz/bad-bot-blocker) and ported to nginx.**

**blacklist.conf** utilizes the following two nginx modules to achieve the same results as the original **bad-bot-blocker**: `ngx_http_geo_module` and `ngx_http_map_module`. This provides admins with a single configuraiton file used for blacklisting any bots or malicious web crawlers.

----

### Install
1. Save `blacklist.conf` somewhere accessible by nginx.
2. Include `blacklist.conf` in your `nginx.conf` before your server blocks.
3. Add the following in each server block you wish to apply the blacklist to:
    ```
    if ($bad_client) {
      return 403;
    }
    ```

### Configure

#### geo $validate_agent block
This contains the list of **IP Addresses** that should be allowed to use any **User-Agent** blocked. By default, it will block all IP addresses using any of the matching IP addresses.

Syntax:
```
  127.0.0.1                      0; 
```
Note: `0` = allow and `1` = deny.


#### geo $validate_client block
This contains the list of **IP Addresses** that should be blocked from accessing the site. This is used to check all IP addresses that don't match any of the offending User-Agent listed. By default, it will allow all IP addresses to do not match any current rules to access the site.

Syntax:
```
  127.0.0.1                      1;
```
Note: `0` = allow and `1` = deny.
