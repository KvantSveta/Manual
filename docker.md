# Docker

- docker search имя_образа (ubuntu)

- docker tag image_id account_name/image_name:version_or_tag

регистрация на Docker Hub

- docker login

получение образа из docker registry

- docker pull имя_образа

- docker run -d имя_образа команда_которая_будет_выполняться_в_контейнере

посмотреть все контейнеры

- docker ps -a

- docker commit ID_контейнера имя_нового_образа

посмотреть детали контейнера

- docker inspect ID_контейнера

список всех образов на этом хосте

- docker images

- docker info

- docker run --name имя_нового_образа (habr) -i -t имя_образа (ubuntu)  /bin/bash

- docker attach имя_образа

- docker logs ID_контейнера/имя_контейнера

- docker stop/kill/start ID_контейнера/имя_контейнера

удалить не нужные контейнеры

- docker rm ID_контейнера

- docker cp путь_к_данным_на_хосте имя_контейнера : путь

- docker run -v /tmp:/root -t -i имя_образа (ubuntu)

отправка образа в docker registry

- docker push имя_пользователя/имя_образа

команда для подключения к docker-контейнеру

- docker exec ID_контейнера/имя_образа

- docker save -o имя_образа.img имя_образа

- docker load -i имя_образа.img

- docker build -t имя_нового_образа путь_к_dockerfile

- docker rmi -f IMAGE_ID

история формирования слоев образа

- docker history имя_образа

статистику использования ресурсов

- docker stats Имя/ID-контейнера

информация о запущенных конейнерах, с указанием используемого дискового пространства

- docker ps -s

информация о всех образах и контейнерах

- docker system df

подробная информация о всех образах и контейнерах

- docker system df -v

очистка от неиспользуемых контейнеров, сетей, образов и кэша

- docker system prune

удаление неныжных volume`ов

- docker volume prune

посмотреть размер директории

```bash
du -sh /var/lib/docker/volumes
```

> -d — «демонизирует» контейнер, то есть просто отключает Docker от STDOUT виртуального окружения и позволяет ему работать в фоне;
--name — имя контейнера, которое он получит вместо идентификатора;
-e — позволяет «пробросить» в виртуалку переменную окружения;
-v — пробрасывает указанный файл или каталог (формат /файл/на/хост/системе:/файл/в/виртуалке или просто /файл/на/хост/системе, если пути совпадают).
-i (STDIN) 
-t (терминал)
-p порт_контейнера:порт_хоста  --restart=always перезапуск контейнера в случае падения
--rm запуск контейнера с удалением его по завершению оного
-m 256m ограничение контейнера в 256 МБ ОЗУ
-с 1024 задать вес контейнера с [1; 1024]; 1024 - max
--cpuset="0,1" ограничить контейнер первыми двумя ядрами

> FROM <имя-образа> — какой образ использовать в качестве базы (должна быть первой строкой в любом Dockerfile).
RUN <команда> — запустить указанную команду внутри контейнера.
CMD <команда> — выполнить команду при запуске контейнера (обычно идет последней).
EXPOSE <порт> — список портов, которые будет слушать контейнер (используется механизмом линковки).
ENV <ключ> <значение> — создать переменную окружения.
ADD <путь> <путь> — скопировать файл/каталог внутрь контейнера/образа (первый аргумент может быть URL).
ENTRYPOINT <команда> — команда для запуска приложения в контейнере (по умолчанию /bin/sh -c).
VOLUME <путь> — пробросить в контейнер указанный каталог (аналог опции -v).
USER <имя> — сменить юзера внутри контейнера.
WORKDIR <путь> — сменить каталог внутри контейнера.
ONBUILD [ИНСТРУКЦИЯ] — запустить указанную инструкцию Dockerfile только в том случае, если образ используется для сборки другого образа (с помощью FROM).

> docker RESTful API tcp:2375, 2376

> Docker Compose - утилита для объединения нескольких контейнеров в одно веб-приложение. Docker Compose удобен для создания приложений, в которых несколько контейнеров объединены и именно совместно представляют собой разрабатываемое приложение.

> Docker Swarm служит для объединения множества Docker хостов в один виртуальный хост и делает это элегантно.

## multi-stage builds

### 1 пример

> FROM golang:latest as build
>
> COPY . .
>
> RUN go build ./src/main.go

---

> FROM alpine:latest as production
>
> COPY --from=build /go/main .
>
> CMD ["./main"]

```bash
docker image build -t hello_world:latest .
```

### 2 пример

Стадия сборки "build-env"

> FROM golang:1.8.1-alpine AS build-env
>
> RUN apk add --no-cache git make
>
> ADD . /go/src/github.com/username/project
>
> WORKDIR /go/src/github.com/username/project
>
> RUN make build

---

Стадия подготовки image к бою

> FROM alpine:3.5
>
> COPY --from=build-env /go/src/github.com/username/project/bin/service /usr/local/bin/service
>
> EXPOSE 65122
>
> CMD ["service"]

### 3 пример

> FROM golang:1.7.3
>
> #FROM golang:1.7.3 as builder
>
> WORKDIR /go/src/github.com/alexellis/href-counter/
>
> RUN go get -d -v golang.org/x/net/html  
>
> COPY app.go .
>
> RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

---

> FROM alpine:latest  
>
> RUN apk --no-cache add ca-certificates
>
> WORKDIR /root/
>
> COPY --from=0 /go/src/github.com/alexellis/href-counter/app .
>
> #COPY --from=builder /go/src/github.com/alexellis/href-counter/app .
>
> CMD ["./app"]

```bash
docker build -t alexellis2/href-counter:latest .
#docker build -t alexellis2/href-counter:latest .
```
