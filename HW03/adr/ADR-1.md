# ADR-1: WEB-приложение "Проверка работ студентов" на основе фреймворка Jmix

## Дата

20.01.2024
## Статус

==Предложено==
## Контекст

Университету нужна автоматизация оценки заданий по программированию. На реализацию выделен очень маленький бюджет.
Приложение должно интегрироваться с системой обнаружения плагиата TurnItIn  и системой управления обучением университета LMS

**Характеристики приложения:**
- не нуждается в масштабировании и высокой производительности
- простая модель данных
- не предполагается сложных SQL-запросов к базе данных
- это небольшая система для малого количества пользователей
- веб-интерфейс
## Решение

**Jmix** - платформа быстрой разработки бизнес-приложений на Java с низким порогом входа  
https://www.jmix.io/
- Ядро фреймворка Jmix реализовано на Spring
- Для разработки достаточно знать только Java
- Один разработчик может делать все - от создания модели данных и бизнес-логики до проектирования интерфейса
- Готовые визуальные компоненты на основе Vaadin. Можно использовать любые компоненты Vaadin
- Маркетплейс дополнений
- REST API
- Возможность использовать библиотеки и коннекторы к инструментам экосистем Spring и Java
- Возможность использовать при разработке сторонние JavaScript / TypeScript / CSS 
- Аутентификация и авторизация пользователей с помощью встроенных средств, возможность использования внешнего провайдера OIDC (например, KeyCloak)
- Есть бесплатная версия
- Apache License 2.0
## Последствия

- Увеличение производительности команды
- Можно использовать менее квалифицированных разработчиков

- **Желательна платная RAD лицензия в стадии активной разработки проекта**, чтобы получить все преимущества разработки Jmix:  
	конструктор модели данных, конструктор экранов, механизм миграции базы данных, конструктор запросов к данным.  
	
	Стоимость 90$ на 1 разработчика в месяц https://www.jmix.io/subscription-plans-and-prices/
	
	*На этапе поддержки готового приложения платная лицензия не нужна*

- Чтобы разрабатывать и собирать проект после истечения подписки Enterprise, нужен приватный репозиторий артефактов, пока подписка еще активна https://docs.jmix.io/jmix/private-artifact-repository.html

- Можно воспользоваться стандартными настройками интерфейса для экономии, при расширении бюджета настроить интерфейс "под себя"
- Интерфейсы настройки прав пользователей "из коробки"
- В дальнейшем систему легко расширять, интегрировать с другими системами, т.к. Jmix дает возможность разработчику пользоваться всей экосистемой Spring и Java

**Минусы:**
- Низкая производительность JPA при использовании сложных моделей данных.  SQL-запросы, генерируемые через JPA, используемый в Jmix, плохо поддаются оптимизации

	*Некритично, т.к. простая модель данных приложения должна свести к минимуму необходимость оптимизации SQL*
	
- Количество одновременно подключенных пользователей до 10 000
	_Некритично, т.к. предполагается 300+ студентов в год, плюс персонал и администратор_