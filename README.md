# Laboratorium nr 10
Sterowniki sieciowe w środowisku docker. Tworzenie i wykorzystanie sieci mostkowych
definiowanych przez użytkownika. Wolumeny i ich podział. Współdzielenie wolumenów.
Integracja systemów plików hosta i kontenera - wolumeny typu bind mount

## Tworzę nową sieć Docker o nazwie lab10net. Używa drivera bridge, co oznacza,
## że sieć będzie działać jako most, umożliwiając komunikację między kontenerami na tej samej sieci.
## Definiuje zakres adresów IP dla sieci (od 10.0.10.1 do 10.0.10.254).

`docker network create --driver=bridge --subnet=10.0.10.0/24 lab10net`


![image](https://github.com/miloszpiechota/lab10/assets/161620373/4c05e651-b5aa-45d4-8c1c-f2f7e754e2e9)


## Tworzenie wolumenu Docker

`docker volume create nginx-vol`

## Uruchamianie kontenera Docker
## Używam typu montowania bind, który pozwala na montowanie plików lub katalogów z hosta do kontenera.
## Określam lokalizację pliku na hoście i lokalizację w kontenerze, gdzie plik będzie zamontowany. Zastępuje domyślną stronę główną Nginx.
## readonly: Montuje plik w trybie tylko do odczytu


`docker run -d --name=web1 --network=lab10net -p 4001:80 --mount type=bind,source=C:\lab10\web1\web1.html,target=/usr/share/nginx/html/index.html,readonly
--mount type=bind,source=C:\lab10\logs\web1_logs,target=/var/log/nginx nginx:latest`


![image](https://github.com/miloszpiechota/lab10/assets/161620373/2c6be615-737e-453f-8bcd-b62f74ca3844)


## Wynik działania aplikacji:
![image](https://github.com/miloszpiechota/lab10/assets/161620373/065bdeb5-5c9c-4d73-aca2-e2e9780ae14c)

![image](https://github.com/miloszpiechota/lab10/assets/161620373/a768bcd2-cdb3-4b2e-8344-e0bedcf74bf9)

![image](https://github.com/miloszpiechota/lab10/assets/161620373/b5be5f86-285f-4542-b767-21847d705f18)

![image](https://github.com/miloszpiechota/lab10/assets/161620373/1ddf429a-18cd-4417-abb2-e71cf966c154)

![image](https://github.com/miloszpiechota/lab10/assets/161620373/1ed980bb-2cc9-4eaa-8b4f-0dbe0c4032d8)

`docker inspect web1`


![image](https://github.com/miloszpiechota/lab10/assets/161620373/51a9bcb0-c288-4961-9c91-16e357c8a3dd)
