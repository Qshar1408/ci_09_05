# Домашнее задание к занятию 11 «Teamcity»

### Грибанов Антон. FOPS-31

## Подготовка к выполнению

1. В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`.
2. Дождитесь запуска teamcity, выполните первоначальную настройку.
3. Создайте ещё один инстанс (2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему переменную окружения `SERVER_URL: "http://<teamcity_url>:8111"`.
4. Авторизуйте агент.
5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity).
6. Создайте VM (2CPU4RAM) и запустите [playbook](./infrastructure).

#### Решение:

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_001.png)

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_002.png)

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_003.png)

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_004.png)

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_005.png)

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_006.png)

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_007.png)


## Основная часть

1. Создайте новый проект в teamcity на основе fork.

#### Создал новый проект на основе fork:

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_008.png)

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_009.png)

2. Сделайте autodetect конфигурации.

#### Выполнил autodetect конфигурации, тип проекта определил как Maven:

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_010.png)

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_011.png)

3. Сохраните необходимые шаги, запустите первую сборку master.

#### Запускаю сборку, сборка выполнена успешно:

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_012.png)

4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`.

#### Поменял условия сборки

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_013.png)

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_014.png)

5. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.

#### Загрузил settings.xml

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_015.png)

6. В pom.xml необходимо поменять ссылки на репозиторий и nexus.
7. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.

#### Запустил сборку, сборка завершилась успешно и артефакт появился в Nexus

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_016.png)

8. Мигрируйте `build configuration` в репозиторий.

#### Мигрировал build configuration в репозиторий

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_017.png)

#### Ссылка [Ссылка](https://github.com/Qshar1408/example-teamcity/tree/master/.teamcity/Netology_ExampleTeamcity)

9. Создайте отдельную ветку `feature/add_reply` в репозитории.

#### Создал отдельную ветку

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_018.png)

11. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`.

#### Написал новый метод для класса Welcomer

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_019.png)

12. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.

#### Дополнил тест для нового метода 

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_020.png)

13. Сделайте push всех изменений в новую ветку репозитория.
14. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.

#### Сборка запустилась, тесты прошли успешно:

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_022.png)

15. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_023.png)

16. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.
17. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.
18. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_024.png)

![ci_09_005](https://github.com/Qshar1408/ci_09_05/blob/main/img/ci_09_025.png)

19. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.
20. В ответе пришлите ссылку на репозиторий.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.
