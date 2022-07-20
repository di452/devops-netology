# Домашнее задание к занятию "5.1. Введение в виртуализацию. Типы и функции гипервизоров. Обзор рынка вендоров и областей применения."

## Задача 1

Опишите кратко, как вы поняли: в чем основное отличие полной (аппаратной) виртуализации, паравиртуализации и виртуализации на основе ОС.

## Ответ: 
Основное отличие как будет построена работа гипервизора. (Поверх ОС, не требуется ОС, в ОС) 

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

## Ответ
 - [физические сервера]() (Высоконагруженная база данных, чувствительная к отказу, системы, выполняющие высокопроизводительные расчеты на GPU)
аппаратное размещение дает более высокий отклик, и сокращает точки отказа гипервизора хостовой машины, либо использование полной аппаратной виртуализации.
быстрый доступ к аппаратным ресурсам.
 - [паравиртуализация]() (Windows системы для использования бухгалтерским отделом) организация бекапа баз данных, возможность расширении ресурсов на уровне вирт. машины.
 - [виртуализация уровня ОС]() (Различные web-приложения)  потребность в ресурсах меньше, скорость масштабирования выше и нет жестких требований к аппаратнымм ресурсам, требует меньше ресурсов на администрирование.


## Задача 3

Выберите подходящую систему управления виртуализацией для предложенного сценария. Детально опишите ваш выбор.

Сценарии:

1. 100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. Преимущественно Windows based инфраструктура, требуется реализация программных балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.
2. Требуется наиболее производительное бесплатное open source решение для виртуализации небольшой (20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.
3. Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации Windows инфраструктуры.
4. Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.

## Ответ

1. Считаю что VMware vSphere подходит наилучшем для данного сценария. Нет ограничений по выбору операционной системы,Содержит необходимые компонеты: планировщик ресурсов, стек хранения данных.
2. Считаю лучше подойдет Xen. позволяет запускать как Linux, так и Windows, обладает высокой производительностью и стабильностью, достаточно надежен как универсальный гипервизор.
3. Hyper-V он по умолчанию идет для всего на Windows.
4. KVM лучшее решение для Linux. 

## Задача 4

Опишите возможные проблемы и недостатки гетерогенной среды виртуализации (использования нескольких систем управления виртуализацией одновременно) и что необходимо сделать для минимизации этих рисков и проблем. Если бы у вас был выбор, то создавали бы вы гетерогенную среду или нет? Мотивируйте ваш ответ примерами.
Проблемы и недостатки:

Проблемы и недостатки:

- сложность в управлении и настройке;
- высокий порог входа для инженеров;
- неэффективность в долгосрочной перспективе (сложность настройки автоматизации и управлении);
- сложность в настройке миграции данных.

Возможные решения:

- использование комплексных решений;
- снижение вероятности несовместимости и маштабируемости (лучший подбор технологий в рамках среды);
использование универсальных платформ. Гетерогенную среду можно использовать в малом бизнесе для уменьшения затрат и времени на развертку. Также возможно использование для низко загруженных приложений.