# Инструкция по развертыванию

## Разворачивание в docker-compose для разработки
  1. Открыть папку проекта в терминале  
    - ввести команды по очереди:
      ```
      docker-compose up -d --build
      ```  
      ```
      docker-compose exec web python3 manage.py collectstatic --no-input --clear
      ```

## Разворачивание в docker-compose для деплоя 
<details><summary>Команды</summary>
<p>

```
  docker-compose -f docker-compose.prod.yml down -v
```
```
  docker-compose -f docker-compose.prod.yml up -d --build
```
```
  docker-compose -f docker-compose.prod.yml exec web python manage.py collectstatic --no-input --clear
```

</p>
</details>