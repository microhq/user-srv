# User Server

A user service for storing accounts and simple auth.

## Getting started

1. Run Consul
2. Run MySQL
3. Run service

	```shell
	go get github.com/micro/user-srv
	```

	```shell
	user-srv --database_url="root:root@tcp(192.168.99.100:3306)/user"

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
micro query go.micro.srv.user Account.Create '{"user":{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b", "username": "asim", "email": "asim@example.com"}, "password": "password1"}'
```

### Account.Read

```shell
micro query go.micro.srv.user Account.Read '{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b"}'
```

### Account.Update

```shell
micro query go.micro.srv.user Account.Update '{"user":{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b", "username": "asim", "email": "asim+update@example.com"}}'
```

### Account.UpdatePassword

```shell
micro query go.micro.srv.user Account.UpdatePassword '{"userId": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b", "oldPassword": "password1", "newPassword": "newpassword1", "confirmPassword": "newpassword1" }'
```

### Account.Delete

```shell
micro query go.micro.srv.user Account.Delete '{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b"}'
```

### Account.Login

```shell
micro query go.micro.srv.user Account.Login '{"username": "asim", "password": "password1"}'
```

### Account.ReadSession

```shell
micro query go.micro.srv.user Account.ReadSession '{"sessionId": "sr7UEBmIMg5hYOgiljnhrd4XLsnalNewBV9KzpZ9aD8w37b3jRmEujGtKGcGlXPg1yYoSHR3RLy66ugglw0tofTNGm57NrNYUHsFxfwuGC6pvCn8BecB7aEF6UxTyVFq"}'
```

### Account.Logout

```shell
micro query go.micro.srv.user Account.Logout '{"sessionId": "sr7UEBmIMg5hYOgiljnhrd4XLsnalNewBV9KzpZ9aD8w37b3jRmEujGtKGcGlXPg1yYoSHR3RLy66ugglw0tofTNGm57NrNYUHsFxfwuGC6pvCn8BecB7aEF6UxTyVFq"}'
```
