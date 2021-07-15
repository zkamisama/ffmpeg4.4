# ffmpeg4.4

## build

```
  docker build . -t ffmpeg4.4:scratch
```

## use other images 
```
  FROM ffmpeg4.4:scratch as ffmpeg
  
  FROM alpine:3.14
  
  WORKDIR /app
  
  RUN  sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
       apk add --no-cache --update libgcc libstdc++ libcrypto1.1 libssl1.1 libgomp expat
       
 ENV   LD_LIBRARY_PATH=/usr/local/lib:/usr/local/lib6
 
 COPY --from=ffmpeg /usr/local /usr/local
 
 CMD ["/bin/sh"]
```
