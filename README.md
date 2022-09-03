# NEAR-Stake_Wars-3

NEAR-Stake Wars Episode-3

Stake Wars — это программа, которая помогает сообществу ознакомиться с тем, что значит быть валидатором NEAR, 

и дает им ранний шанс получить доступ к Сhunk-only producer. 

Вознаграждения, предлагаемые программой Stake Wars, поддерживают новых участников,

которые хотят присоединиться к основной сети в качестве валидатора, начиная с сентября 2022 года.

Цель стимулированной тестовой сети - тестирование сети, чтобы удостовериться, что она надежна и оптимизирована для высокой производительности.

Войны ставок начались 13 июля и продлятся 9 сентября 2022 года . Вы можете присоединиться в любой момент. 

Задания добавляются в течение всего периода программы, следите за обновлениями. 

По условиям конкурса, для получения вознаграждений может потребоваться проверка личности (KYC).

Подробные правила участия можно прочитать тут: https://github.com/near/stakewars-iii/blob/main/rules.md

Для участия необходимо заполнить форму участника: https://nearprotocol1001.typeform.com/to/Z39N7cU9?typeform-source

Минимальные требования к оборудованию:

CPU: 4-Core CPU with AVX support

RAM: 8GB DDR4

Storage: 500GB SSD

Я выбрал выделенный сервер от известного хостера HETZNER, модель AX41-NVME.

Данный сервер обладает высокой производительностью и запасом мощности для данного этапа тестирования.

Посмотреть цены и выбрать себе сервер можно по ссылке: https://www.hetzner.com/ru/dedicated-rootserver/matrix-ax

![1](https://user-images.githubusercontent.com/78436658/187992176-af5ba0c8-d53e-4d4d-8a20-469f05ecc19f.jpg)

После необходимо создать кошелек в сети NEAR Shardnet.

Переходим для этого по ссылке: https://wallet.shardnet.near.org/

![1](https://user-images.githubusercontent.com/78436658/187992632-07372754-efae-4214-8231-ceb5711280b9.jpg)

![1](https://user-images.githubusercontent.com/78436658/187993164-30db30e2-d6ed-4a30-8bc4-c3d6c4aa116f.jpg)

Когда кошелек успешно создан, на него сразу придут тестовые токены, которые будут необходимы для дальнейших задач.

![1](https://user-images.githubusercontent.com/78436658/187993457-527e50d5-d5f6-4bb1-8d8b-f1100df165e6.jpg)

Переходим на сервер и теперь рабоатаем в командной строке.

В данном примере я делаю установку под суперпользователем root , операционная система ubuntu 20.04 lts 

Сначала надо обновить пакеты:

sudo apt update && sudo apt upgrade -y

Установить Node.js и npm:

curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -

sudo apt install build-essential nodejs

PATH=”$PATH”

Проверить версии (нужна версия не ниже 18.х.х.):

node -v

npm -v

Установить NEAR-CLI:

sudo npm install -g near-cli

Настроить необходимую окружающую среду:

export NEAR_ENV=shardnet

echo ‘export NEAR_ENV=shardnet’ >> ~/.bashrc

echo ‘export NEAR_ENV=shardnet’ >> ~/.profile

Поставить необходимые инструменты разработчика:

sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python docker.io protobuf-compiler libssl-dev pkg-config 
clang llvm cargo

Установить Python pip:

sudo apt install python3-pip

Установить конфигурацию:

USER_BASE_BIN=$(python3 -m site — user-base)/bin

export PATH=”$USER_BASE_BIN:$PATH”

Установить Building env:

sudo apt install clang build-essential make

Установить Rust & Cargo:

curl — proto ‘=https’ — tlsv1.2 -sSf https://sh.rustup.rs | sh

в появившемся списке выбрать “1”

![1](https://user-images.githubusercontent.com/78436658/187995037-101f5eb5-4210-4220-b73a-cafe11e44f29.jpg)

source $HOME/.cargo/env

Склонировать nearcore репозиторий:

git clone https://github.com/near/nearcore

cd nearcore

git fetch

Проверить актуальный comit по ссылке https://github.com/near/stakewars-iii/blob/main/commit.md

Добавить его:

git checkout <commit>
  
В моем случае это выглядит так: git checkout 8448ad1ebf27731a43397686103aa5277e7f2fcf
  
Скомпилировать бинарный файл:
  
cargo build -p neard --release --features shardnet
  
Инициализировать рабочую директорию:
  
./target/release/neard --home ~/.near init --chain-id shardnet --download-genesis
  
Заменить файл config.json:
  
rm ~/.near/config.json
  
wget -O ~/.near/config.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/config.json
  
Установить AWS CLI:
  
sudo apt-get install awscli -y
  
Заменить файл genesis.json предварительно удалив старый:
  
rm ~/.near/genesis.json
  
cd ~/.near 
  
wget https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/genesis.json

 Авторизовать кошелек локально, для этого ввести в командной строке:
  
cd
  
near login  
  
![1](https://user-images.githubusercontent.com/78436658/187995977-6ea043a2-53c7-44a9-9557-35d4fb0b51b8.jpg)
  
скопировать ссылку из командной строки и вставить в строку браузера где установлен кошелек near.
  
![1](https://user-images.githubusercontent.com/78436658/187996711-ac24547a-c220-4a07-85de-2932de01373d.jpg)
  
подтвердить действие и дождаться вот такого экрана:
  
![1](https://user-images.githubusercontent.com/78436658/187996918-677dc1b9-7b3a-4377-8797-f967b99eb459.jpg)

  Перейти в терминал и ввести имя своего кошелька , в моем случае это neonik690.shardnet.near
  
Когда соединение будет установлено, появится надпись successfully.
  
Создать файл validator_key.json:
  
near generate-key <pool_id>
  
Придумать свое имя пула и подставить убрав кавычки
  
мой пример:
  
near generate-key neonik690.factory.shardnet.near
  
Cкопировать файл из папки shardnet в папку .near и назвать его validator_key.json:
  
cp ~/.near-credentials/shardnet/YOUR_WALLET.json ~/.near/validator_key.json
  
YOUR_WALLET — имя кошелька (мой пример neonik690.shardrnet.near)
  
Отредактировать файл validator_key.json как показано у меня на скриншоте ниже :
  
nano ~/.near/validator_key.json
  
![1](https://user-images.githubusercontent.com/78436658/187998698-9bbc1223-6d2e-46c7-b140-ca950b806a38.jpg)
  
Сохранить сделанные изменения ctrl +S и выйти из редакотора ctrl + X

  Создать сервисный файл:
  
sudo nano /etc/systemd/system/neard.service
  
[Unit]
  
Description=NEARd Daemon Service
  
[Service]
  
Type=simple
  
User=root
  
#Group=near
  
WorkingDirectory=/root/.near
  
ExecStart=/root/nearcore/target/release/neard run
  
Restart=on-failure
  
RestartSec=20
  
KillSignal=SIGINT
  
TimeoutStopSec=40
  
KillMode=mixed
  
[Install]
  
WantedBy=multi-user.target

Сохранить и выйти из редактора.
  
systemctl daemon-reload
  
Активировать сервис: 
  
systemctl enable neard
  
Запустить узел:
  
systemctl start neard
  
Проверить логи узла и сделать их цветными:
  
apt install ccze
  
journalctl -n 100 -f -u neard | ccze -A
  
Необходимо дождаться полной синхронизации и только потом переходить к следующему этапу.

  Развернуть пул ставок:
  
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": ""pool id"", "owner_id": ""accountId"", "stake_public_key": ""public key"", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId=""accountId"" --amount=450 --gas=300000000000000

Где вместо <pool id> <public key> и <accountId> подставить свои данные
  
 ""public key"" - взять из файла командой
  
cat ~/.near/validator_key.json
  
 ""pool id"" - имя стейкинг пула
  
 ""accountId"" - имя кошелька
  
 Мой пример: near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "x690", "owner_id": "neonik690.shardnet.near", "stake_public_key": "ed25519:2AcDiCwYMuhHM8PrhbyPyAf43RNT5pfN3FdPQRvkafgH", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="neonik690.shardnet.near" --amount=450 --gas=300000000000000
  
Проверить свой пул в эксплорере браузера можно по ссылке https://explorer.shardnet.near.org/nodes/validators

 Внести депозит и сделать ставку:
  
near call ИМЯПУЛА.factory.shardnet.near deposit_and_stake --amount 100 --accountId ИМЯКОШЕЛЬКА.shardnet.near --gas=300000000000000
  
100 - количество вносимых токенов

 Разделегировать ставку можно командой:
  
near call <pool_id> unstake ‘{“amount”: “<amount yoctoNEAR>”}’ --accountId <accountId> --gas=300000000000000
  
где <amount yoctoNEAR> это необходимое количество монет к разделегированию.

 Разделегировать все:
  
near call <pool_id> unstake_all --accountId <accountId> --gas=300000000000000

 Вывод с узла занимает 2–3 эпохи:
  
near call <pool_id> withdraw ‘{“amount”: “<amount yoctoNEAR>”}’ --accountId <accountId> --gas=300000000000000
  
где <amount yoctoNEAR> это необходимое количество монет к разделегированию.

 Если нужно вывести все, то использовать команду ниже:
  
near call <pool_id> withdraw_all --accountId <accountId> --gas=300000000000000

 Пинг узла.
  
Пинг выдает новое предложение и обновляет баланс ставок для ваших делегатов. Пинг должен выдаваться каждую эпоху, чтобы сообщаемые награды были актуальными.

near call <pool_id> ping ‘{}’ --accountId <accountId> --gas=300000000000000
  
- <accountId> - имя кошелька

RPC
  
Любой узел в сети предлагает услуги RPC на порту 3030, пока порт открыт в брандмауэре узлов.
  
Обычно RPC используется для проверки статистики валидатора, версии узла и просмотра доли делегатора, 
  
хотя ее можно использовать для взаимодействия с блокчейном, учетными записями и контрактами в целом.
  
Более подробно о многих командах и о том, как их использовать, читайте здесь:
  
https://docs.near.org/api/rpc/introduction
  
 Проверить версию узла:
  
curl -s http://127.0.0.1:3030/status | jq .version

 Проверить делегаторов и ставки:
  
near view <your pool>.factory.shardnet.near get_accounts ‘{“from_index”: 0, “limit”: 10}’ — accountId <accountId>.shardnet.near

 Проверить причину отказа узла:
  
curl -s -d ‘{“jsonrpc”: “2.0”, “method”: “validators”, “id”: “dontcare”, “params”: [null]}’ -H ‘Content-Type: application/json’ 127.0.0.1:3030 | jq -c ‘.result.prev_epoch_kickout[] | select(.account_id | contains (“<POOL_ID>”))’ | jq .reason
  
 Основные команды NEAR CLI для работы с узлом:
  
 Предложение валидатора указывает на то, что он хотел бы войти в набор валидатора, 
  
чтобы предложение было принято, оно должно соответствовать минимальной цене места.
  
 Использовать команду:
  
near proposals

 Cписок активных валидаторов в текущую эпоху, количество произведенных блоков,
  
количество ожидаемых блоков и скорость онлайн. 
  
 Использовать команду:
  
near validators current
  
 Валидаторы, чье предложение было принято одну эпоху назад и которые войдут в набор валидаторов в следующую эпоху
  
 Использовать команду:
  
near validators next
 
 Еще больше полезных команд и коментариев к ним:
  
 Использовать команду:
  
near -help
  
![1](https://user-images.githubusercontent.com/78436658/188003888-07ffa750-ee54-4304-b001-2abb5e0b551e.jpg)


 
  
  
  
  


 
  
  
















