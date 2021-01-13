# Faircorp Frontend

[Deployed Frontend on EMSE Gitlab Pages](http://alexandre.verdet.gitlab.emse.fr/wmp-frontend/)

- Author : Alexandre Verdet, Erwan Tinen and Shaokun Xie
- VueJS Frontend App of the 2020 Web & Mobile Programing project for [EMSE's Computer Science Major](https://ci.mines-stetienne.fr/m-info/wmp/)
- Based on [Quentin Richaud's course](https://gitlab.com/emse1/cours_js_1)

## Context

The goal of the 2020 Web & Mobile Programing project is to implement a fully functionnal Building management system (especially rooms, windows and heaters controllers).\
The project is composed of a [Java SpringBoot Backend server](https://github.com/averdet/faircorp-spring-app), an [Android Kotlin Application](https://github.com/averdet/faircorp-android-app) and a [VueJS Frontend server](https://github.com/averdet/faircorp-vue-app) interacting together. An extension of this project can be made with Arduinos Controlers in the [IoT course](https://ci.mines-stetienne.fr/m-info/iot/), in order to actually control devices.


## Project setup or access via the [Deployed Gitlab Page](http://alexandre.verdet.gitlab.emse.fr/wmp-frontend/)
Install all the dependencies

```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

You can now access the frontend on [localhost:8080](http://localhost:8080)

NB : the frontend is supposed to work with the [Spring Backend](https://github.com/averdet/faircorp-spring-app) deployed on Clever-Cloud. If not or if you want to run the backend locally, you can configure the API's hostname in [./src/config.js](./src/config.js)

### Compiles and minifies for production
```
npm run build
```


