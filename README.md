## Задача 1

Опишите кратко, как вы поняли: в чем основное отличие полной (аппаратной) виртуализации, паравиртуализации и виртуализации на основе ОС.

### Ответ:
При полной виртуализации гостевая операционная система работает поверх гипервизора, установленного на «голом железе». Гость не знает, что он виртуализируется и не требует никаких изменений для работы в этой конфигурации. И наоборот, при паравиртуализации гостевая операционная система не только знает, что она работает на гипервизоре, но и включает код для более эффективного перехода от гостевой системы к гипервизору.

В схеме полной виртуализации гипервизор должен эмулировать аппаратное обеспечение устройства, которое эмулируется на самом низком уровне. В схеме паравиртуализации гость и гипервизор могут работать совместно, чтобы сделать эту эмуляцию эффективной. Недостатком подхода паравиртуализации является то, что операционная система знает, что она виртуализируется, и для ее работы требуются модификации.

Виртуализация на основе ОС позволяет запускать изолированные "контейнеры" на хосте. Программы, работающие внутри контейнера, могут видеть только содержимое контейнера и устройства, назначенные контейнеру. Контейнер обращается  без гипервизора в ОС.

## Задача 2

Выберите один из вариантов использования организации физических серверов, в зависимости от условий использования.

Организация серверов:
- физические сервера,
- паравиртуализация,
- виртуализация уровня ОС.

Условия использования:
- Высоконагруженная база данных, чувствительная к отказу.
- Различные web-приложения.
- Windows системы для использования бухгалтерским отделом.
- Системы, выполняющие высокопроизводительные расчеты на GPU.

Опишите, почему вы выбрали к каждому целевому использованию такую организацию.

### Ответ:
- Высоконагруженная база данных, чувствительная к отказу: - физические сервера, все таки высоконагруженная, но обычно для удобства это аппаратная виртуализация типа ESXI, относительно быстрый бэкап и восстановление
- Различные web-приложения: виртуализация уровня ОС, скорость работы не в приоритете, в приоритете скорость развертывания, "привет, Docker!
- Windows системы для использования бухгалтерским отделом: здесь паравиртуализация, там и с лицензиями попроще
- Системы, выполняющие высокопроизводительные расчеты на GPU: физические сервера, все выжать из ресурсов

## Задача 3

Выберите подходящую систему управления виртуализацией для предложенного сценария. Детально опишите ваш выбор.

Сценарии:

1. 100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. Преимущественно Windows based инфраструктура, требуется реализация программных балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.
2. Требуется наиболее производительное бесплатное open source решение для виртуализации небольшой (20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.
3. Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации Windows инфраструктуры.
4. Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.

### Ответ:
1.Решения от VMWare, прикрутить туда бэкап от Veeam и вперед, в продакшн! 
2.Бесплатное решение KVM - и бесплатно, и для Linux и Windows подойдет.
3.Hyper-V, использовать существующие лицензии, решение максимально совместимое для Windows.
4.Будем тестировать в Docker-контейнерах, на образах разных систем - запустил, потестировал скриптами, удалил

## Задача 4

Опишите возможные проблемы и недостатки гетерогенной среды виртуализации (использования нескольких систем управления виртуализацией одновременно) и что необходимо сделать для минимизации этих рисков и проблем. Если бы у вас был выбор, то создавали бы вы гетерогенную среду или нет? Мотивируйте ваш ответ примерами.

### Ответ:
Проблемы:
1. Децентрализация - разные консоли управления
2. Разделение ресурсов между системами
3. Различные компетенции

Для минимизации рисков - структурированая строгая система бэкапа, начиная от регламентов резервного копирования, хранения данных, восстановления при авариях. Запас по ресурсам аппаратной части системы бэкапа. Повышение квалификации персонала (внутренне и внешнее обучение).

При моем личном выборе была бы не гомогенная среда конечно, а пара сред - одна превалирует, основная, другая служит для специфических проектов. 80/20 - как-то так.
Сама жизнь не даст зациклиться на одной среде - обязательно появится проект, требующий что-то свое, не вписывающийся в существующий ай-ти ландшафт.
