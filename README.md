# User Server

User server is a microservice to store user accounts and perform simple authentication.

## Getting started

1. Install Consul

	Consul is the default registry/discovery for go-micro apps. It's however pluggable.
	[https://www.consul.io/intro/getting-started/install.html](https://www.consul.io/intro/getting-started/install.html)

2. Run Consul
	```
	$ consul agent -server -bootstrap-expect 1 -data-dir /tmp/consul
	```

3. Start a mysql database

4. Download and start the service

	```shell
	go get github.com/micro/user-srv
	user-srv --database_url="root:root@tcp(192.168.99.100:3306)/user"
	```

	OR as a docker container

	```shell
	docker run microhq/user-srv --database_url="root:root@tcp(192.168.99.100:3306)/user" --registry_address=YOUR_REGISTRY_ADDRESS
	```

## The API
User server implements the following RPC Methods

Account
- Create
- Read
- Update
- Delete
- Search
- UpdatePassword
- Login
- Logout
- ReadSession


### Account.Create
```shell
$ micro query go.micro.srv.user Account.Create '{"user":{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b", "username": "asim", "email": "asim@example.com"}, "password": "password1"}'
{}
```

### Account.Read
```shell
$ micro query go.micro.srv.user Account.Read '{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b"}'
{
	"user": {
		"created": 1.450816182e+09,
		"email": "asim@example.com",
		"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b",
		"updated": 1.450816182e+09,
		"username": "asim"
	}
}
```

### Account.Update
```shell
$ micro query go.micro.srv.user Account.Update '{"user":{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b", "username": "asim", "email": "asim+update@example.com"}}'
{}
```

### Account.UpdatePassword
```shell
$ micro query go.micro.srv.user Account.UpdatePassword '{"userId": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b", "oldPassword": "password1", "newPassword": "newpassword1", "confirmPassword": "newpassword1" }'
{}
```

### Account.Delete
```shell
$ micro query go.micro.srv.user Account.Delete '{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b"}'
{}
```

### Account.Login
```shell
$ micro query go.micro.srv.user Account.Login '{"username": "asim", "password": "password1"}'
{
	"session": {
		"created": 1.450816852e+09,
		"expires": 1.451421652e+09,
		"id": "sr7UEBmIMg5hYOgiljnhrd4XLsnalNewBV9KzpZ9aD8w37b3jRmEujGtKGcGlXPg1yYoSHR3RLy66ugglw0tofTNGm57NrNYUHsFxfwuGC6pvCn8BecB7aEF6UxTyVFq",
		"username": "asim"
	}
}
```

### Account.ReadSession
```shell
$ micro query go.micro.srv.user Account.ReadSession '{"sessionId": "sr7UEBmIMg5hYOgiljnhrd4XLsnalNewBV9KzpZ9aD8w37b3jRmEujGtKGcGlXPg1yYoSHR3RLy66ugglw0tofTNGm57NrNYUHsFxfwuGC6pvCn8BecB7aEF6UxTyVFq"}'
{
	"session": {
		"created": 1.450816852e+09,
		"expires": 1.451421652e+09,
		"id": "sr7UEBmIMg5hYOgiljnhrd4XLsnalNewBV9KzpZ9aD8w37b3jRmEujGtKGcGlXPg1yYoSHR3RLy66ugglw0tofTNGm57NrNYUHsFxfwuGC6pvCn8BecB7aEF6UxTyVFq",
		"username": "asim"
	}
}
```

### Account.Logout
```shell
$ micro query go.micro.srv.user Account.Logout '{"sessionId": "sr7UEBmIMg5hYOgiljnhrd4XLsnalNewBV9KzpZ9aD8w37b3jRmEujGtKGcGlXPg1yYoSHR3RLy66ugglw0tofTNGm57NrNYUHsFxfwuGC6pvCn8BecB7aEF6UxTyVFq"}'
{}
```
