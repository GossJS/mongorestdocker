Итак, были задания для самостоятельного исследования

1. Исследуйте сопоставление томов (volumes), так чтобы после работы контейнера mongodb данные, собранные через веб-интерфейс, были доступны в папке извне контейнера для дальнейшего повторного использования

2. Дополните конфигурацию docker-compose контейнером nginx так, чтобы nginx служил прокси запросов с порта 80 на тот, на котором работает наше API (например 3000)

Соответственно для пользователя запрос к API будет выглядеть более кратким:



1. Создаём скейлет с приложением-докером и подключаемся через .ssh

(если есть домен, то оперативно изменяем его DNS-зону с учётом полученного IP)

```
Если нужно сгенерировать ключи

ssh-keygen -t rsa 

в конец публичного ключа добавляется имя_юзера@имя_компа

например vscale1@air

micro id_rsa.pub -  в настройках скейлета нужно найти SSH-ключи и добавить новый или при создании скейлета 
``` 

2. Выполняем

git clone -b mongorestvolume 'https://github.com/GossJS/mongorestdocker.git' /sites

3. Переходим в /sites/data и распаковываем templates_12112017.zip

4. Переходим в /sites и делаем docker-compose up

Теперь по корневому маршруту у нас будут доступны файлы из папки /sites/data для скачивания

А по адресу http://95.213.199.198/alldocuments/templates?apiKey=ifna212ASFisfsjaAFFF

будет доступно то, что известно как http://95.213.199.198:3000/api/templates?apiKey=ifna212ASFisfsjaAFFF

И можно отправлять API-запросы используя этот адрес.

Затем можно зазиповать получившееся содержимое папки  /data и использовать уже этот архив на следующей итерации. Или сделать экспорт.

---
Доступ через имя домена требует изменения файла конфигурации default.conf (допустим домен у нас ikoder.xyz)

      listen 1234 ikoder.xyz "";
      listen [::]:1234 ikoder.xyz "";
      
Если этого не сделать, получим 502 - Bad Gateway - потому что то, что написано справа от listen с номером порта - это то, что сопоставляется с полем Host - по этому признаку сервер определяет, какую из конфигураций server использовать. Пустота в кавычках говорит серверу, что нужно использовать ту же самую конфигурацию при обращении просто по IP.


Следующая задача - обеспечить доступ по SSL/TLS




