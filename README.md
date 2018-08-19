# User Server

A user service for storing accounts and simple auth.

## Getting started

To run this example, make sure that you have Consul and MySQL running.

### Install package

To easily run this example, you can install this repository as a Go package using the following command in your terminal.

```shell
go get github.com/microhq/user-srv
```
	
If you run into problems installing the `usr-srv` package, make sure that you have git terminal prompts enabled.

```shell
env GIT_TERMINAL_PROMPT=1 go get github.com/microhq/user-srv
```

### Run service

Run the service using the `usr-srv` binary installed in the previous step. Also, make sure that the `$GOPATH/bin` directory is listed on your environment `$PATH`. 

```shell
user-srv --database_url="root:root@tcp(127.0.0.1:3306)/user"
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


### Create

```shell
micro query go.micro.srv.user Account.Create '{"user":{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b", "username": "asim", "email": "asim@example.com"}, "password": "password1"}'
```

### Read

```shell
micro query go.micro.srv.user Account.Read '{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b"}'
```

### Update

```shell
micro query go.micro.srv.user Account.Update '{"user":{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b", "username": "asim", "email": "asim+update@example.com"}}'
```

### Update Password

```shell
micro query go.micro.srv.user Account.UpdatePassword '{"userId": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b", "oldPassword": "password1", "newPassword": "newpassword1", "confirmPassword": "newpassword1" }'
```

### Delete

```shell
micro query go.micro.srv.user Account.Delete '{"id": "ff3c06de-9e43-41c7-9bab-578f6b4ad32b"}'
```

### Login

```shell
micro query go.micro.srv.user Account.Login '{"username": "asim", "password": "password1"}'
```

### Read Session

```shell
micro query go.micro.srv.user Account.ReadSession '{"sessionId": "sr7UEBmIMg5hYOgiljnhrd4XLsnalNewBV9KzpZ9aD8w37b3jRmEujGtKGcGlXPg1yYoSHR3RLy66ugglw0tofTNGm57NrNYUHsFxfwuGC6pvCn8BecB7aEF6UxTyVFq"}'
```

### Logout

```shell
micro query go.micro.srv.user Account.Logout '{"sessionId": "sr7UEBmIMg5hYOgiljnhrd4XLsnalNewBV9KzpZ9aD8w37b3jRmEujGtKGcGlXPg1yYoSHR3RLy66ugglw0tofTNGm57NrNYUHsFxfwuGC6pvCn8BecB7aEF6UxTyVFq"}'
```
