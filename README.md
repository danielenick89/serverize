# serverize
A little tool to (http)server-ize any shell command

## Security
**Serverize is a security threat. Not ready for production and probably never will be - it's a testing tool to be used in a secure environment. Use it very carefully.**  
Serverize is used to expose a shell command via http. Doesn't require authentication, it doesn't implement any encryption and relies on python's *subprocess* library to make sure it doesn't expose a whole shell to the network. Anyway, by default it only listens on the loopback device thus only allowing requests from localhost.  

## What
Serverize is a test tool that can be used to expose a shell command to the local network via http. It spins up an http server, and for every requests it executes the given command with the given path passed as parameters.

An example is better than a thousand words:  
`serverize ls`
will expose the command ls to the network. Thus calling the endpoint http://localhost:8000//home/user/ will execute the command `ls /home/user/` and return the output the command as http response.

### Other examples

`serverize echo`  
will send back whatever you pass as GET path (actally everything after the first `/` in the request, and `&`s will be translated to spaces)  

`serverize python myscript.py`  
you can pass a command which has its own parameters, the http parameters will be appended after

`serverize curl`  
will basically create a very basic proxy


Any `&` will be translated to spaces. 

## Why
It happened many times to me that I had prototyped something on my computer and I wanted to quickly interface this to other components (a web server running somewhere else, a PHP script, etc.) to test it or make a proof of concept. Serverize was born like this, since it's pretty easy to make a simple http request: you can curl, file_get_contents(), or even ajax your command in this way. In testing times, it can be a way to avoid headaches with user permissions, reachability from a different host, or simply avoid using os.system("mycommand") or equivalent which can be unsafe if used lightly. Still remember this was not thought to be a serious, reliable or secure tool. 

## Installation
Make sure you have Python 3+ installed on your system. Then download the file and make it executable (`chmod +x serverize` on linux/mac). You might want to move it in your `PATH` to use it from anywhere.

## Usage
`serverize [-p port] <command> `

if not specified, the default port is 8000
