禁用第三方cookie，并非禁用所有cookie
第三方cookie指的是，非当前站点提供的cookie，因为用户访问多个使用同一第三方cookie的网站时，第三方可以获取到多个站点的信息，暴露用户信息。

如果要继续使用第三方cookie，需要在Set-Cookie中设置`Partitioned`属性。

Cookie技术面临淘汰，如果打算替换Cookie，可行的替代技术方案有：
- token放在请求头，存储在localStorage、sessionStorage、indexDB等位置。
- FedCM