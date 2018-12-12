# Docker build	
Let’s walk through manually building a Docker image so we can see the benefits of using a Compose file. 

Start by reviewing the `Dockerfile`
```
FROM alpine
RUN apk add --no-cache perl
COPY cowsay /usr/local/bin/cowsay
COPY docker.cow /usr/local/share/cows/default.cow
ENTRYPOINT ["/usr/local/bin/cowsay"]
```

Now we need to add execute permissions to the `cowsay` binary
```
chmod +x cowsay 
```

Now build the Docker image

```
docker build -t <hubusername>/cowsay . 
```

You should see the image build quickly. 

Let’s go ahead and run it. 
```
docker run <hubusername>/cowsay cowsay boo
```

If everything was successful you should see something similar to: 

```
 ____________ 
< cowsay boo >
 ------------ 
    \
     \
      \
                    ##         .
              ## ## ##        ==
           ## ## ## ## ##    ===
       /"""""""""""""""""\___/ ===
      {                       /  ===-
       \______ O           __/
         \    \         __/
          \____\_______/

```

Congrats you’ve built a Docker image! 

