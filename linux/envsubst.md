# envsubst is greedy

##### Source: `pain and suffering (minor)`

Sadly, nginx does not provide access to Environment variables in its config by default. Thus, if you were wanting to pull deployment information from the Env, you're basically out of luck, unless you want to get [quite hacky][1].

Happily, in a Docker deployment there exists a not-quite-as-awful™ approach which is to use `envsubst` (part of the `gettext` package) and [substitute your variables][2] as part of the Docker CMD.

Today's learning is that if you have any kind of variable in the config indicated by a $ prefix, envsubst will replace that with an empty string if said variable doesn't exist in the Environment. Boo. And particularly Boo since we're using [nginx-rtmp][3] and it likes to use $vars for various things.

The solution is to specify the vars you want to replace as arguments to the `envsubst` invocation. Thus, instead of
```
envsubst < /usr/local/nginx/conf/nginx.templ > /usr/local/nginx/conf/nginx.conf && nginx -g 'daemon off;'
```
you'd use
```
envsubst '$API_HOST' < /usr/local/nginx/conf/nginx.templ > /usr/local/nginx/conf/nginx.conf && nginx -g 'daemon off;'
```

[1]: http://serverfault.com/questions/577370/how-can-i-use-environment-variables-in-nginx-conf
[2]: https://github.com/docker-library/docs/tree/master/nginx#using-environment-variables-in-nginx-configuration
[3]: https://github.com/arut/nginx-rtmp-module