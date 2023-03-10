# SJournal_ERD
Диаграмма зависимостей для БД Student Logbook

## Таблицы и значения их атрибутов
### `Sys_role`
Справочная таблица системных ролей
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник
 + name: String - Название системной роли
### `User`
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
### `Group`
Таблица, содержащая информацию о учебных группах
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник
 + name: String - название группы
 + id_user_lead: Integer (Foreign Key) - айдишник пользователя-старосты учебной группы
 + id_user_supervisor: Integer (Foreign Key) - айдишник пользователя-кураторы учебной группы
### `Student`
Таблица, содержащая информацию о студентах
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник
 + first_name: String - имя студента
 + middle_name: String - отчетство студента
 + last_name: String - фамилия студента
 + id_group: Integer (Foreign Key) - айдишник учебной группы, к которой привязан студент
### `LessonNumber`
Справочная таблица, содержащая информацию о временных рамках занятий
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник, обозначающий пару по счёту
 + time_start: TIME - время начала пары
 + time_end: TIME - время конца пары
### `Subject`
Справочная таблица, содержащая информацию по учебным дисциплинам
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник
 + name: String - название дисциплины, Прим. "Прикладное программирование"
 + code: String - кодовое название дисциплины, Прим. "МДК.01.02"
### `TimetableLesson`
Справочная таблица, содержащая расписание занятий по группам
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник
 + id_group: Integer (Foreign Key) - айдишник учебной группы, которая должна присутствовать на занятии
 + id_user_teacher: Integer (Foreign Key) - айдишник пользователя-преподавателя, который по умолчанию ведёт занятие у вписанной группы
 + id_lesson_number: Integer (Foreign Key) - айдишник пары, которой по счёту в расписании стоит занятие
 + id_subject: Integer (Foreign Key) - айдишник дисциплины, которая будет на занятии
 + day_of_week: Integer - день недели, в который будет проведено занятие
 + week_num: Integer - неделя по счёту, (По дефолту 0 или 1, соответственно в реалности 1 или 2) для вариации расписания между неделями как в настоящем расписании
### `Lesson`
Таблица, содержащая информацию о проведённом занятии
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник
 + id_timetable_lesson: Integer (Foreign Key) - айдишник занятия в расписании
 + description: String - тема занятия
 + id_rep_teacher: Integer (Foreign Key) - айдишник пользователя-преподавателя, на замене, если такой понадобится, по умолчанию значение NULL, если замены не было
### `AbscentStudent`
Таблица, содержащая информацию о отсутствующих студентах, на определённом занятии
#### Атрибуты
 + id_lesson: Integer (Primary Key - Foreign Key) - айдишник проводимого занятия
 + id_user_writer: Integer (Primary Key - Foreign Key) - айдишник пользователя, оставившего запись, чтобы потом была возможность сверить показания, поскольку в реальности присутствующих отмечают одновременно два человека: преподаватель и староста.
 + id_student: Integer (Foreign Key) - айдишник отсутствующего студента
 + count_of_hours: Integer - количество пропущенных часов на занятии у студента (1 или 2)
### `Mark`
Таблица, содержащая информацию о оценках, полученных студентами на проведённом занятии
#### Атрибуты
 + id: Integer (Primary Key) - обычный уникальный айдишник
 + id_student: Integer (Foreign Key) - айдишник студента, получившего оценку
 + mark: Integer - оценка
 + id_lesson: Integer (Foreign Key) - айдишник занятия, на котором студент получил оценку
