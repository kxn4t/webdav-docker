# webdav-docker
A simply WebDAV docker image.  
WebDAV LOCK can also be used.  
use digest authentication.  

# Usage
## run
`docker run -dit --name=webdav -v <path to location>:/usr/local/apache2/uploads -p 8080:80 kxn4t/webdav-docker`  
non mount (temporary using)  
`docker run -dit --name=webdav -p 8080:80 kxn4t/webdav-docker`  

## access
`http://localhost/uploads`

One person is registered as an initial user.  
user: admin  
pass: test1234  

## change password
1. docker exec  
`docker exec -it webdav bash`  

2. change htdigest  
`htdigest "/usr/local/apache2/user.passwd" DAV-upload admin`  

3. change password

4. restart httpd  
`httpd -k restart`

## add user
1. docker exec  
`docker exec -it webdav bash`  

2. change httpd-dav.conf  
`vim conf/extra/httpd-dav.conf`
```
    <RequireAny>
        Require method GET POST OPTIONS LOCK
        Require user admin <add username>
    </RequireAny>
```
example:
```
    <RequireAny>
        Require method GET POST OPTIONS LOCK
        Require user admin kxn4t
    </RequireAny>
```

3. add htdigest  
`htdigest "/usr/local/apache2/user.passwd" DAV-upload <add username>`  

4. restart httpd  
`httpd -k restart`  

# License
MIT
