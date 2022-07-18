# virt-homeworks

# Домашнее задание к занятию "5.1. Основы виртуализации"

## Задача 1

Вкратце опишите, как вы поняли - в чем основное отличие паравиртуализации и виртуализации на основе ОС.

## Ответ 1:
Пожалуй, главное отличие паравиртуализации от виртуализации на основе ОС состоит в том, что при последней у нас созданные машины используют ядро родительской операционки, а значит это не позволяет создавать виртуалки с ядром отличным от ядра родителя. При паравиртуализации мы не используем ядро родителя напрямую, а значит можем создавать любые виртуалки без этой привязки.

## Задача 2

Выберите тип один из вариантов использования организации физических серверов, 
в зависимости от условий использования.

Организация серверов:
- физические сервера
- паравиртуализация
- виртуализация уровня ОС

Условия использования:

- Высоконагруженная база данных, чувствительная к отказу
- Различные Java-приложения
- Windows системы для использования Бухгалтерским отделом 
- Системы, выполняющие высокопроизводительные расчеты на GPU

Опишите, почему вы выбрали к каждому целевому использованию такую организацию.

## Ответ 2:
**Высоконагруженная база данных, чувствительная к отказу** - физические сервера или полная (аппаратная виртуализация) типа VMware с нормальным бекап решением типа Veeam, поскольку при таком способе максимальное количество точек отказа минимально, а количество ресурсов доступных системе максимально.

**Различные Java-приложения** - виртуализация уровня ОС. При таком способе приложение разрабатывается в изолированных контейнерах со всеми обвязками. Поэтому ускоряется возможность разворачивать приложения в проде, а также многократно упрощается возможность их маштабирования если нагрузка на этот сервис возрастет.

**Windows системы для использования Бухгалтерским отделом** - Паравиртуализация от Microsoft hyper-v в режиме службы в данном случае оптимально, поскольку это нативное и относительно решение для Windows от Windows же.

**Системы, выполняющие высокопроизводительные расчеты на GPU** - в зависимости от задач можно использовать разные стстемы. Физические сервера позволяют не терять ресурсы на виртуализации, с друго стороны паравиртуализация может позволить собрать несколько физических серверов в одно логическое и использовать эту абстракцию для управления всеми GPU сразу, например.

## Задача 3

Как вы думаете, возможно ли совмещать несколько типов виртуализации на одном сервере?
Приведите пример такого совмещения.

## Ответ 3:
Я думаю, что да. На работе я использую железные сервера собранные с помощью гипервизора Proxmox в кластер - это паравиртуализации. В кластере у меня подняты, как обычные виртуалки с установленным на них докером и подманом, так и линукс контейнеры (LXC). Это уже пример виртуализации уровня ОС.

