# Docker
- [CMD vs ENTRYPOINT](#cmd_vs_entrypoint)

## CMD vs ENTRYPOINT <a name="cmd_vs_entrypoint"></a>
Both CMD and ENTRYPOINT are used to run a command at the end of running docker image. Both CMD and ENTRYPOINT are used to run a command at the end of the docker image launch. CMD parameters can be overridden, ENTRYPOINT can't and always will be run. Using both in one focker file will result in CMD being the default parameter for ENTRYPOINT. Examples:
``` dockerfile 
FROM ubuntu
CMD ["echo", "Hello World"]
```
``` 
docker run file-name
-> Hello World

docker run file-name echo "Message Changed"
-> Message Changed
```
***

``` dockerfile 
FROM ubuntu
ENTRYPOINT ["echo", "Hello World"]
```
``` 
docker run file-name
-> Hello World

docker run file-name echo
-> Hello World echo
```
***
``` dockerfile
FROM ubuntu
ENTRYPOINT ["echo", "Hello"]
CMD ["World"]
```
``` 
docker run file-name
-> Hello World

docker run file-name echo
-> Hello echo
```