# serverize
A little tool to (http)server-ize any shell command

## Security
**Serverize is a security threat. Not ready for production and probably never will be - it's a testing tool to be used in a secure environment. Use it very carefully.**
Serverize is used to expose a shell command via http. Doesn't require authentication, it doesn't implement any encryption and relies on python's *subprocess* library to make sure it doesn't expose a whole shell to the network. Anyway, by default it only listens on the loopback device thus only allowing requests from localhost. 

## Why
Serverize is a test tool that can be used to expose a shell command to the local network via http. It spins up an http server, and for every requests it executes the given command with the given path passed as parameters.

An example is better than a thousand words:
`serverize ls`
will expose the command ls to the network. Thus calling the endpoint http://localhost:8000//home/user/ will execute the command `ls /home/user/` and return the output the command as http response.

`serverize curl` will basically create a very basic proxy 

Any & will be translated to spaces. 

## Usage
`serverize [-p port] <command> `
`
if not specified, the default port is 8000
