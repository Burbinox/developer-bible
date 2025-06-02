# Docker
- [CMD vs ENTRYPOINT vs RUN](#cmd_vs_entrypoint)
- [Layers](#layers)

## CMD vs ENTRYPOINT <a name="cmd_vs_entrypoint"></a>
RUN used to execute commands during image building. 
Both CMD and ENTRYPOINT are used to run a command at the end of the docker image launch. CMD parameters can be overridden, ENTRYPOINT can't and always will be run. Using both in one docker file will result in CMD being the default parameter for ENTRYPOINT. Examples:
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

## Layers <a name="layers"></a>
Each command in Dockerfile is a new layer which is also a cache. If there are no changes in layer docker during build command it uses cached version of a layer. So the order matter. Example:

``` dockerfile 
FROM pyton:3.8                         # Layer n
WORKDIR /code                          # Layer n + 1
COPY requirements.txtx .               # Layer n + 2
RUN pip install -r ./requirements.txt  # Layer n + 3
COPY python_file.py .                  # Layer n + 4
CMD ["python", "./python_file.py"]     # Layer n + 5
```