---
creation date: 2023-01-11 15:39
modification date: Wednesday, 11th January 2023, 15:39:02
tags: today_i_leaned, engineering/yocto, engineering/devops/webserver, engineering/embedded/petalinux
---

# How to add and customize nginx in Yocto

---
## Step 1 - Add nginx to your project.

_for my project, I am using petalinux, so it may differ in your setup_

Under `project-spec/meta-user/conf`, add the following to the `user-rootfsconfig` file.

```
CONFIG_nginx
```

Run `petalinux-config -c rootfs` and select nginx; under user packages.

![Pasted image 20230111155131](attachments/Pasted%20image%2020230111155131.png)

---
## Step 2 - Create the nginx custom recipe.

In your project-spec folder, create an nginx folder for your customization.

```shell
mkdir -p project-spec/meta-user/recipes-httpd/nginx/files
touch project-spec/meta-user/recipes-httpd/nginx/nginx_%.bbappend
```

The path to the `nginx_%.bbappend` can be anything you want, as long as it is within your Yocto layer.

In the custom nginx recipe, enter the following:

```bitbake
FILESEXTRAPATHS:prepend := "${THISDIR}/files:"
 
SRC_URI:append = " \
	file://my_server \
"

do_install:append(){
	install -d ${D}${sysconfdir}/nginx/sites-available
	install -D -m 644 ${WORKDIR}/my_server ${D}${sysconfdir}/nginx/sites-available/

	# Remove the default server config; otherwise my_server will
	# conflict since it is also on port 80.
	rm -rf ${D}${sysconfdir}/nginx/sites-enabled/default_server

	ln -s ${sysconfdir}/nginx/sites-available/spa_server ${D}${sysconfdir}/nginx/sites-enabled/
}
```

This configuration removes the default server from `sites-enabled` and places my server as the default server.

---
## Step 3 - Create the nginx server config file.

Put the following in the file `project-spec/meta-user/recipes-httpd/files/my_server`

```nginx
server {
    listen 80 default_server;
    listen [::]:80 default_server;


    root /var/www/path_to_my_server_react_spa;
    index index.html index.htm;

    server_name _;

    # redirect server error pages to the static page /50x.html
    error_page 500 502 503 504 /50x.html;

    # ref: https://gist.github.com/aotimme/5006831
    location / {
        try_files $uri $uri/ /index.html =404;
    }

}
```