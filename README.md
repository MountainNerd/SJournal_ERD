# SJournal_ERD
Диаграмма зависимостей для БД Student Logbook

## Таблицы и значения их атрибутов
### Sys_role
Справочная таблица системных ролей
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник
 + name: String - Название системной роли
### User
Таблица пользователей системы
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник
 + username: String - логин пользователя
 + password: String - пароль пользователя
 + id_sys_role: Integer (Foreign Key) - айдишник роли пользователя в системе
 + first_name: String - имя пользователя
 + middle_name: String - отчетство пользователя
 + last_name: String - фамилия пользователя
 + email: String - эл. почта пользователя
### Group
Таблица содержащая информацию о учебных группах
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник
 + name: String - название группы
 + id_user_lead: Integer (Foreign Key) - айдишник пользователя-старосты учебной группы
 + id_user_supervisor: Integer (Foreign Key) - айдишник пользователя-кураторы учебной группы
