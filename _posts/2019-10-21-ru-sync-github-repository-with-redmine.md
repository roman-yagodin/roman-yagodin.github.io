---
layout: post
category: how-to
title: "Синхронизация GitHub с хранилищем Redmine"
tagline: "Sync your GitHub code repository with Redmine"
tags : [GitHub, Redmine, Git]
---
{% include JB/setup %}

Описывается процесс настройки синхронизации репозитория исходного кода на GitHub с хранилищем в проекте Redmine с использованием плагина [Redmine GitHub Hook](http://www.redmine.org/plugins/redmine_github_hook) на примере [репозитория темы Greenmine](http://projects.volgau.com/projects/greenmine/repository).

<!-- more -->

* * * * *

## Создание зеркала

Создаем зеркало публичного репозитория GitHub:

```Shell
sudo -u redmine /bin/bash
cd /var/opt/redmine/repos
git clone --mirror https://github.com/volgau/redmine-theme-greenmine.git
```

Добавляем в проект новое хранилище, связанное с зеркалом репозитория, через меню **Настройки проекта > Хранилища**.

<img src="{{ site.url }}/assets/images/ru-sync-github-repository-with-redmine-1.png" alt="Создание нового хранилища в Redmine" class="img-responsive" />

## Настройка синхронизации

В настройках проекта на GitHub (меню **Settings > Webhooks**) добавляем новый webhook.

**Внимание!** Параметр **project_id** в **Payload URL** устанавливаем равным идентификатору проекта, а не хранилища!

Если в проекте несколько хранилищ, то добавляем к URL параметр **repository_id**. Возможные форматы URL см. в [readme плагина](https://github.com/koppen/redmine_github_hook#readme)

<img src="{{ site.url }}/assets/images/ru-sync-github-repository-with-redmine-2.png" alt="Добавляем webhook в GitHub" class="img-responsive" />

Если все настроено правильно, то все изменения состояния кода в удаленном репозитории на GitHub будут автоматически отражаться в локальном зеркале, а коммиты будет добавлены в [историю действий](http://projects.volgau.com/projects/greenmine/activity?from=2018-01-30).

Если что-то пошло не так (статус отправки изменений можно посмотреть в разделе **Recent Deliveries**), то лучше всего выполнить настройку сначала - проверить настройки на стороне Redmine, удалить и заново добавить webhook на GitHub.
