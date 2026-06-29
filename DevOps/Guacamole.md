# Guacamole (guacd, postgresql, guacamole)

```yml
version: '3.8'

networks:
  guacnetwork_compose:
    driver: bridge

services:
  guacd:
    container_name: guacd_compose
    image: guacamole/guacd:latest
    restart: unless-stopped
    networks:
      - guacnetwork_compose
    volumes:
      - ./drive:/drive:rw
      - ./record:/record:rw

  postgres:
    container_name: postgres_guacamole_compose
    image: postgres:15-alpine
    restart: unless-stopped
    networks:
      - guacnetwork_compose
    environment:
      POSTGRES_DB: guacamole_db
      POSTGRES_USER: guacamole_user
      POSTGRES_PASSWORD: 'ChooseYourOwnPasswordHere1234' # Ваш пароль
      # PGDATA УДАЛЕН ОТСЮДА
    volumes:
      - ./initdb.sql:/docker-entrypoint-initdb.d/initdb.sql:ro
      - ./postgres_data:/var/lib/postgresql/data

  guacamole:
    container_name: guacamole_compose
    image: guacamole/guacamole:latest
    restart: unless-stopped
    networks:
      - guacnetwork_compose
    depends_on:
      - guacd
      - postgres
    environment:
      GUACD_HOSTNAME: guacd
      # ИСПРАВЛЕННЫЕ ПЕРЕМЕННЫЕ (POSTGRESQL вместо POSTGRES):
      POSTGRESQL_HOSTNAME: postgres
      POSTGRESQL_PORT: 5432
      POSTGRESQL_DATABASE: guacamole_db
      POSTGRESQL_USERNAME: guacamole_user
      POSTGRESQL_PASSWORD: 'ChooseYourOwnPasswordHere1234' # Пароль должен совпадать с POSTGRES_PASSWORD выше
      RECORDING_SEARCH_PATH: /record
    volumes:
      - ./record:/record:rw
    ports:
      - "8080:8080/tcp"
    group_add:
      - "1000"
```