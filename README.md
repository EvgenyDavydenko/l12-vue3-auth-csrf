## Laravel12 Vue3 создание блога с авторизацией на основе CSRF защиты

1.  Creating a Laravel Project
```
composer create-project laravel/laravel ./
```
2.   Install Laravel Sanctum
```
php artisan install:api
rm database/migrations/2025_11_15_134911_create_personal_access_tokens_table.php
php artisan config:publish cors
```
3.  Install Fortify
```
composer require laravel/fortify
php artisan fortify:install
```
4.  Creating a Vue Application with Vue-Router and Axios
```
npm create vue@latest
npm install
npm i axios
```
5.  Настроить подключение к БД в .env
6.  Накатить миграции:
```
php artisan migrate --seed
```
7. Запрос на получение токена и приватный эндпоинт

8. Установить Bootstrap CSS
```
npm i bootstrap@5.3.8
```
9. Реализация аутентификации.

Создать централизованную логику для управления состоянием аутентификации, включая вход, выход и проверку авторизации. Мы используем Composition API для создания реактивного и переиспользуемого модуля src/composables/useAuth.js

Предоставить пользователю интерфейс (форму) src/components/LoginPage.vue для ввода учетных данных и взаимодействия с логикой из useAuth.

Дефолтный пользователь Admin создается на сервере при поднятии контейнера с приложением

10. Показать список постов с пагинацией и страницу конкретного поста для гостей сайта (не требует аутентификации)

11. Создать дашборд для админа с crud операциями
