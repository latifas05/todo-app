Лабораторная работа 3: CI/CD с GitHub Actions
Цель: построить CI/CD-pipeline в GitHub Actions, который после каждого git push запускает тесты, собирает Docker-образ и публикует его на Docker Hub. Логин и токен Docker Hub хранятся в GitHub Secrets, а не в коде.
Ссылка на публичный репозиторий: https://github.com/latifas05/todo-app
Ссылка на успешный запуск pipeline: https://github.com/latifas05/todo-app/actions/runs/39903076029
Ссылка на образ в Docker Hub: https://hub.docker.com/repository/docker/lil1iee/todo-app/general
Структура проекта:
<img width="1140" height="645" alt="1" src="https://github.com/user-attachments/assets/79883dba-a08e-41e9-987f-9dbc2223e2f9" />

1.Какой тест упал в части 3 и что было написано в логе?
<img width="1852" height="870" alt="Screenshot 2026-10-23 101643" src="https://github.com/user-attachments/assets/ec6b0f4e-4110-4942-84fd-b9e4d0c1c305" />
<img width="1847" height="701" alt="Screenshot 2026-10-23 102043" src="https://github.com/user-attachments/assets/e939f2c2-9aa1-44f6-ae17-58c1a505dabc" />
Упал тест test_health, так как эндпоинт вернул статус в верхнем регистре ("OK" вместо "ok"), что вызвало ошибку сравнения в pytest (AssertionError).

2.Почему в части 7 job build-and-push пропущена?
<img width="1422" height="732" alt="Screenshot 2026-10-23 105825" src="https://github.com/user-attachments/assets/21609169-0b25-4929-9dc6-0679140a4fb0" />
Из-за защитного условия if: github.ref_name == 'main' && github.event_name != 'pull_request', которое пропускает этап сборки и публикации при проверке Pull Request, выполняя только тесты.

3.Зачем нужен тег с SHA коммита, если есть latest?
<img width="892" height="967" alt="Screenshot 2026-10-29 003637" src="https://github.com/user-attachments/assets/abe78384-227e-4ac9-8fe1-9b01e354242e" />
Тег latest является перезаписываемым и изменяется при каждом новом деплое. Тег с SHA коммита фиксирует конкретную версию исходного кода, обеспечивая точный аудит, версионирование и возможность быстрого отката (rollback).
