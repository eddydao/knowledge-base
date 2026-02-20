`brew uninstall --force nginx && brew cleanup`: uninstall nginx and clean up

`ls -la /opt/homebrew/etc/nginx/ 2>/dev/null || echo "No nginx config directory found"`: check if there is any configuration file or folder left

`rm -rf /opt/homebrew/etc/nginx`: remove all config if found

`ssh -L 8080:localhost:8080 -p 22 -o ServerAliveInterval=60 -o ServerAliveCountMax=3 thanhdao@eddydao.ddns.net` : forward port 8080 SSH tunnel