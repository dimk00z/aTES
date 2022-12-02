# aTES
Awesome Task Exchange System (aTES) для UberPopug Inc

## Контекст и проблема

Топ-менеджмент UberPopug Inc столкнулся с проблемой производительности сотрудников. Чтобы повысить производительность, было принято решение выкинуть текущий таск-трекер и написать особый Awesome Task Exchange System (aTES), который должен будет увеличить производительность сотрудников на неопределённый процент. Чтобы попуги развивались и изучали новые направления, была придумана инновационная схема ассайна каждой задачи на случайного сотрудника. А для повышения мотивации топ-менеджмент решил сделать корпоративный аккаунтинг в таск-трекере, чтобы по количеству выполненных задач выплачивать сотрудникам зарплату. При этом задачи оцениваются с плавающим коэффициентом (местами отрицательным).

## Общие требования

В ходе обсуждения задачи с топ-менеджментом были выявлены следующие требования:

### Таск-трекер

1. Таск-трекер должен быть отдельным дашбордом и доступен всем сотрудникам компании UberPopug Inc.
2. Авторизация в таск-трекере должна выполняться через общий сервис авторизации UberPopug Inc (у нас там инновационная система авторизации на основе формы клюва).
3. В таск-трекере должны быть только задачи. Проектов, скоупов и спринтов нет, потому что они не умещаются в голове попуга.
4. Новые таски может создавать кто угодно (администратор, начальник, разработчик, менеджер и любая другая роль). У задачи должны быть описание, статус (выполнена или нет) и попуг, на которого заассайнена задача.
5. Менеджеры или администраторы должны иметь кнопку «заассайнить задачи», которая возьмёт все открытые задачи и рандомно заассайнит каждую на любого из сотрудников (кроме менеджера и администратора) . Не успел закрыть задачу до реассайна — сорян, делай следующую.

    a) Ассайнить задачу можно на кого угодно (кроме менеджера и администратора), это может быть любой существующий аккаунт из системы.
    
    b) Ассайнить задачу можно только кнопкой «заассайнить задачи»
    
    c) При нажатии кнопки «заассайнить задачи» все текущие не закрытые задачи должны быть случайным образом перетасованы между каждым аккаунтом в системе
    
    d) Мы не заморачиваемся на ограничение по нажатию на кнопку «заассайнить задачи». Её можно нажимать хоть каждую секунду.
    
    e) На одного сотрудника может выпасть любое количество новых задач, может выпасть ноль, а может и 10.
    
    f) Создать задачу не заасайненую на пользователя нельзя. Т.е. любая задача должна иметь попуга, который ее делает

6. Каждый сотрудник должен иметь возможность видеть в отдельном месте список заассайненных на него задач + отметить задачу выполненной.
###  Аккаунтинг: кто сколько денег заработал

1. Аккаунтинг должен быть в отдельном дашборде и доступным только для администраторов и бухгалтеров.

a) у обычных попугов доступ к аккаунтингу тоже должен быть. Но только к информации о собственных счетах (аудит лог + текущий баланс). У админов и бухгалтеров должен быть доступ к общей статистике по деньгами заработанным (количество заработанных топ-менеджментом за сегодня денег + статистика по дням).

2. Авторизация в дешборде аккаунтинга должна выполняться через общий сервис аутентификации UberPopug Inc.

3. У каждого из сотрудников должен быть свой счёт, который показывает, сколько за сегодня он получил денег. У счёта должен быть аудитлог того, за что были списаны или начислены деньги, с подробным описанием каждой из задач.

4. Расценки:

 - цены на задачу определяется единоразово, в момент появления в системе (можно с минимальной задержкой)
   - цены рассчитываются без привязки к сотруднику
 - формула, которая говорит сколько списать денег с сотрудника при ассайне задачи — rand(-10..-20)$
 - формула, которая говорит сколько начислить денег сотруднику для выполненой задачи — rand(20..40)$
 - деньги списываются сразу после ассайна на сотрудника, а начисляются после выполнения задачи.
отрицательный баланс переносится на следующий день. Единственный способ его погасить - закрыть достаточное количество задач в течение дня.

5. Дешборд должен выводить количество заработанных топ-менеджментом за сегодня денег.
a) т.е. сумма всех закрытых и заасайненых задач за день с противоположным знаком: (sum(completed task amount) + sum(assigned task fee) * -1
6. В конце дня необходимо:
  a) считать сколько денег сотрудник получил за рабочий день

  b) отправлять на почту сумму выплаты.

7. После выплаты баланса (в конце дня) он должен обнуляться, и в аудитлоге всех операций аккаунтинга должно быть отображено, что была выплачена сумма.
8. Дашборд должен выводить информацию по дням, а не за весь период сразу.
a) вообще хватит только за сегодня (всё равно попуги дальше не помнят), но если чувствуете, что успеете сделать аналитику за каждый день недели — будет круто

### Аналитика
1. Аналитика — это отдельный дашборд, доступный только админам.
2. Нужно указывать, сколько заработал топ-менеджмент за сегодня и сколько попугов ушло в минус.
3. Нужно показывать самую дорогую задачу за день, неделю или месяц.

  a) самой дорогой задачей является задача с наивысшей ценой из списка всех закрытых задач за определенный период времени

  b) пример того, как это может выглядеть:

    03.03 — самая дорогая задача — 28$
    02.03 — самая дорогая задача — 38$
    01.03 — самая дорогая задача — 23$
    01-03 марта — самая дорогая задача — 38$

###  Технические дополнения

1. Никакого сложного UI-дизайна не надо, хватит самого банального бутстрапа или чистого html.
2. Никакого реалтайма тоже не нужно, хватит рефреша страницы для всех дашбордов и пользовательского интерфейса.
3. Вопрос нагрузки не стоит, можно считать, что максимальное количество пользователей будет не больше 100 пользователей в минуту.
4. Язык и технологии можно выбрать любые, кроме BrainFuck.
5. Все права на PopugJira принадлежат UberPopug Inc.
6. Желательно, чтобы ни один попуг в ходе выполнения ДЗ не пострадал.