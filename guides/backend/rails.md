# Rails

## Работа со временем

* Не забывайте указывать часовой пояс. 

  Явно задавайте его в `aplication.rb` и это предотвартит лишние вопросы пользователей и потенциальные проблемы, с этим 
  связанные.

  ```ruby
  # config/application.rb:
  class Application < Rails::Application
    config.time_zone = 'Moscow'
  end
  ```

* Получая текущее время или дату, не забывайте про часовой пояс

  ```ruby
  # GOOD! Методы, учитывающие часовой пояс
  2.hours.ago # => Thu, 21 May 2015 13:17:05 MSK +03:00
  1.day.from_now # => Fri, 22 May 2015 15:17:14 MSK +03:00
  Time.zone.now # => Thu, 21 May 2015 15:18:43 MSK +03:00
  Time.current # Более короткий и предпочтительный метод
  Date.today.in_time_zone # => 21 May 2015 00:00:00 MSK +03:00
  Time.zone.today # => Thu, 21 May 2015
  Date.current # Более короткий и предпочтительный метод

  # BAD! Методы не учитывающие часовой пояс
  Time.now # Возвращает системное время без учёта часового пояса
  Date.today # Может вернуть вчерашнюю или сегодняшнюю дату, в зависимости от часового пояса
  Date.today.to_time # Всё ещё не учитывает часовой пояс
  ```
* При работе с введёнными пользователем данными, не забывайте про часовой пояс

  Используйте следующие методы при парсинге полученных от пользователя данных:

  ```ruby
  Time.zone.parse("2012-03-02 16:05:37") # => Fri, 02 Mar 2012 16:05:37 MSK +04:00
  Time.strptime(time_string, "%Y-%m-%dT%H:%M:%S%z").in_time_zone # Если вы не можете использовать предыдущий метод
  ```
