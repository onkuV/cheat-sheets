
First start by mounting the Rclone directory in any location

things to consider:
* Mounted folder permission 
	Solution: Use --allow-others incase nginx is showing not permitted
	and add 'user_allow_other' to /etc/fuse.conf
* Nginx Issue 403
	Solution: set folder permission as root:root


## List all available shared drives/mydrive on gdrive as json

```bash
rclone backend -o config drives remote:
```

Sample rclone usage
```bash
rclone mount remote: /var/www/gdrive \
--fast-list --drive-use-trash=false \
--allow-other --buffer-size 20M \
--cache-dir ./cache --vfs-cache-mode minimal \
--vfs-read-chunk-size 30M --no-checksum \
--drive-use-created-date --drive-chunk-size 16M \
--drive-acknowledge-abuse --drive-skip-dangling-shortcuts

```

## Using rclone to serve the address 
``rclone serve http remote: --addr ip/domain:port --fast-list --buffer-size 20M \
``--cache-dir ./cache --vfs-cache-mode minimal \
``--vfs-read-chunk-size 30M --no-checksum --baseurl "0:" \
``--htpasswd ~/.rclone/.htpasswd

```bash
rclone serve http remote: --addr ip/domain:port --fast-list --buffer-size 20M \
--cache-dir ./cache --vfs-cache-mode minimal \
--drive-use-created-date --drive-chunk-size 16M \
--drive-acknowledge-abuse --drive-skip-dangling-shortcuts \
--vfs-read-chunk-size 30M --no-checksum --baseurl "0:" \
--htpasswd ~/.rclone/.htpasswd
```

serve :  serving the remote drive to
	http : 
-
##Sample Nginx Config for listing rclone directory
```ini
server {
        listen 80 default_server ;
        listen [::]:80 default_server;
        access_log  /var/log/nginx/access.log;
        server_name _;
        root /var/www/gdrive;
        location / {
                autoindex on;
        }

}
```