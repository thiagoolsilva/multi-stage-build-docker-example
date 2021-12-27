# Welcome to multi-stage-build-docker-example 👋
![Version](https://img.shields.io/badge/version-1.0.0-blue.svg?cacheSeconds=2592000)
[![Twitter: thiagoolsilva](https://img.shields.io/twitter/follow/thiagoolsilva.svg?style=social)](https://twitter.com/thiagoolsilva)

> This is a very simple example of the use of multi stage docker build that improves the docker's image size

### 🏠 [Homepage](https://github.com/thiagoolsilva/multi-stage-build-docker-example)


## Why use multi stage docker build?
According to the official documentation, the use of multi stage docker build will help us as the following description.

> One of the most challenging things about building images is keeping the image size down. Each instruction in the Dockerfile adds a layer to the image, and you need to remember to clean up any artifacts you don’t need before moving on to the next layer. To write a really efficient Dockerfile, you have traditionally needed to employ shell tricks and other logic to keep the layers as small as possible and to ensure that each layer has the artifacts it needs from the previous layer and nothing else.

> It was actually very common to have one Dockerfile to use for development (which contained everything needed to build your application), and a slimmed-down one to use for production, which only contained your application and exactly what was needed to run it. This has been referred to as the “builder pattern”. Maintaining two Dockerfiles is not ideal.

Source: https://docs.docker.com/develop/develop-images/multistage-build/


## Which scenarios are recommended to use the multi stage docker?

As described before, I can resume the use of multi docker build in the following use cases.

* Reduce the final docker build image;
* Split the build, Run and etc... to stages phases;
* Cache the build Stages;

# Multi Stage Build

This is a piece of multi stage dockerfile split up in two stages. The first one will create a docker to build the code and the second one will get the output of first one 
using the code `COPY --from=buildStage /app/dist/ /app/` due to improve the final docker image size. 

```
# Stage 1: Build the base code. 
FROM node:14.17.0-alpine as buildStage

LABEL stage="builder"

...

# Stage 2. Run build container code using the code from buildStage phase.
FROM node:14.17.0-alpine
LABEL author="Thiago lopes da Silva<thiagoolsilva@gmail.com>"

...

COPY --from=buildStage /app/dist/ /app/

...
```
[Full dockerfile code](script/docker/dockerfile)


## Do you want more details about this topic?

Please give it a try and go to the post that I've created about this topic in the [medium](https://thiagolopessilva.medium.com/)

> The post was written in the Portuguese language.

## Install

```sh
yarn install
```

## Build

```sh
yarn docker:build-clean
```

## Usage
```sh
yarn docker:run

$output:
The method main() was called.
calling the uuid.v4()
Result: 032e4c47-0635-4e84-87b1-724d6e4be3f1
Done in 0.69s.
```



## Author

👤 **Thiago lopes da silva <thiagoolsilva@gmail.com>**

* Website: https://medium.com/@thiagolopessilva
* Twitter: [@thiagoolsilva](https://twitter.com/thiagoolsilva)
* Github: [@thiagoolsilva](https://github.com/thiagoolsilva)
* LinkedIn: [@https:\/\/www.linkedin.com\/in\/thiago-lopes-silva-2b943a25\/](https://linkedin.com/in/https:\/\/www.linkedin.com\/in\/thiago-lopes-silva-2b943a25\/)

## 🤝 Contributing

Contributions, issues and feature requests are welcome!

Feel free to check [issues page](https://github.com/thiagoolsilva/multi-stage-build-docker-example/issues). 

## Show your support

Give a ⭐️ if this project helped you!


## 📝 License

Copyright © 2021 [Thiago lopes da silva <thiagoolsilva@gmail.com>](https://github.com/thiagoolsilva).

This project is [Apache V2](https://github.com/thiagoolsilva/multi-stage-build-docker-example/blob/main/LICENSE) licensed.

***
_This README was generated with ❤️ by [readme-md-generator](https://github.com/kefranabg/readme-md-generator)_