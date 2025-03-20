# Домашнее задание к занятию «Ansible. Часть 1»


## Задание 1


Какие преимущества даёт подход IAC?

Ответ:

Подход Infrastructure as Code (IaC) предоставляет множество преимуществ, кардинально меняя подход к управлению инфраструктурой. 
Вот основные из них:

Автоматизация и ускорение развёртывания: 
IaC позволяет автоматизировать процесс развёртывания инфраструктуры. Вместо ручного конфигурирования серверов, сетей и других компонентов, мы описываем инфраструктуру в коде (например, YAML, JSON, или специализированные языки, такие как Terraform HCL). После этого процесс развёртывания выполняется автоматически, быстро и предсказуемо. Это значительно ускоряет развёртывание новых сред (development, staging, production), ускоряет релизы и повышает скорость итераций.

Улучшенная согласованность и предсказуемость: Код является единственным источником правды для вашей инфраструктуры. Это гарантирует, что вся инфраструктура будет развернута и сконфигурирована согласованно, вне зависимости от окружения. Изменения в инфраструктуре также контролируются кодом, что снижает риск ошибок, которые часто приводят к рассогласованию конфигураций.

Управляемость версиями (Version Control): Как и любой код, IaC может храниться в системе контроля версий (например, Git). Это дает вам следующие возможности:

Отслеживание изменений:
Мы всегда знаем, когда и какие изменения были внесены в нашу инфраструктуру.
Возможность отката: При возникновении проблем можно легко откатить изменения до предыдущей рабочей версии.
Коллаборация: Несколько членов команды могут работать над инфраструктурой одновременно, используя стандартные процессы работы с кодом (pull requests, code reviews и т.д.).
Аудит и Compliance: Возможность аудита всех изменений, внесенных в инфраструктуру.
Уменьшение ручного труда и ошибок: Автоматизация, предсказуемость и контроль версий снижают потребность в ручном конфигурировании, что, в свою очередь, уменьшает вероятность ошибок. Это экономит время и ресурсы, а также снижает риски простоев и проблем, связанных с неверной конфигурацией.

Повышенная масштабируемость:
IaC упрощает масштабирование инфраструктуры. Мы можем легко создавать новые ресурсы (например, виртуальные машины, базы данных) или изменять их конфигурацию, просто изменяя код и запуская автоматизированный процесс развертывания.

Воспроизводимость (Reproducibility): Мы можем легко воспроизвести свою инфраструктуру в любом окружении (например, для тестирования, разработки или восстановления после сбоя), просто применив тот же код. Это гарантирует, что наша инфраструктура будет работать одинаково в разных окружениях.

Самодокументирование:
Код IaC служит документацией для нашей инфраструктуры. Он описывает, как все компоненты взаимосвязаны, и как они сконфигурированы.

Эффективное управление стоимостью: IaC позволяет более эффективно управлять стоимостью облачной инфраструктуры. Мы можем автоматизировать выключение ненужных ресурсов, оптимизировать конфигурацию, чтобы снизить потребление ресурсов, и легко изменять масштаб в зависимости от потребностей.

Поддержка DevOps практик: IaC является ключевым элементом DevOps, который включает автоматизацию, непрерывную интеграцию/непрерывное развертывание (CI/CD) и collaboration.

В целом, IaC позволяет организациям более эффективно, надежно и быстро управлять своей инфраструктурой, что приводит к ускорению релизов, снижению рисков и повышению общей гибкости и производительности.


## "Задание 2
Выполните действия и приложите скриншоты действий."

Установите Ansible.
Настройте управляемые виртуальные машины, не меньше двух.
Создайте файл inventory с созданными вами ВМ.
Проверьте доступность хостов с помощью модуля ping.

![Снимок экрана (584)](https://github.com/user-attachments/assets/e0bfda36-52d5-4ddd-98a0-a6ed59dc86ae)

![Снимок экрана (585)](https://github.com/user-attachments/assets/2cae4b5b-47a1-4c7f-ade0-1d8b408f5ba8)

![Снимок экрана (586)](https://github.com/user-attachments/assets/2095670b-44c7-41e2-bc07-fac80056bf79)

![Снимок экрана (587)](https://github.com/user-attachments/assets/9c50dc6f-2256-4171-969d-9f12770b57cd)



## Задание 3

Какая разница между параметрами forks и serial?

Ответ:

1. forks:

Назначение: forks контролирует степень параллелизма, которую Ansible использует при выполнении задач. Определяет максимальное количество хостов, к которым Ansible будет пытаться подключиться и выполнять задачи одновременно .
Область действия: forks это настройка, которая влияет на весь запуск Ansible . Она может быть установлена:
В ansible.cfgфайле (глобально).
Использование параметра командной строки -fили при запуске .--forksansible-playbook
Значение по умолчанию: Значение по умолчанию для forksобычно равно 5. Это означает, что Ansible попытается выполнить задачи на 5 хостах одновременно.
Влияние:
Увеличениеforks : может ускорить выполнение playbook, особенно когда задачи связаны с вводом-выводом (например, копирование файлов). Однако это также может увеличить нагрузку на ваш узел управления Ansible и управляемые хосты.
Уменьшениеforks : может уменьшить нагрузку, но увеличить общее время выполнения. Полезно, когда ваш узел управления или управляемые хосты имеют ограниченные ресурсы.

2. serial:

Назначение: serial управляет размером пакета , когда вы хотите выполнять задачи в непрерывных обновлениях или пакетах . Он определяет , сколько хостов Ansible будет обновлять за раз, прежде чем перейти к следующему пакету .
Область действия: serial — это настройка уровня воспроизведения . Вы устанавливаете ее в файле playbook в определенном play.
Значения: serial могут быть:
Положительное целое число (например, serial: 3). Это означает, что Ansible будет обновлять 3 хоста одновременно.
Процент (например, serial: "30%"). Это означает, что Ansible обновит 30% хостов в каждом пакете.
"1": Это гарантирует, что одновременно обновляется только один хост (полностью последовательно).

Влияние:
Последовательные обновления : serialимеют решающее значение для выполнения последовательных обновлений, когда вы хотите обновлять свои серверы пакетами, чтобы свести к минимуму время простоя и потенциальные сбои.
Управление ресурсами : полезно, когда вы хотите ограничить влияние задачи на вашу инфраструктуру (например, перезапустить службу только на нескольких машинах одновременно, чтобы избежать перегрузки системы).

Пример
```
- hosts: webservers
  serial: "20%"
  tasks:
    - name: Update web server
      apt:
        name: apache2
        state: latest
```
В этом примере Ansible обновит apache2пакет на 20% хостов в webserversгруппе за раз. Если у вас 10 веб-серверов, Ansible обновит 2 сервера, затем еще 2 и т. д.


## Задание 4
В этом задании вы будете работать с Ad-hoc коммандами.

Выполните действия и приложите скриншоты запуска команд.

Установите на управляемых хостах любой пакет, которого нет.
Проверьте статус любого, присутствующего на управляемой машине, сервиса.
Создайте файл с содержимым «I like Linux» по пути /tmp/netology.txt.
