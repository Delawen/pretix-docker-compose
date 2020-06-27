# Pretix Development Environment

### Start it up

* update your config file at ./etc/pretix.cfg
* `docker-compose up` to run development environment 

### Modifications to parent repo

* We create ./etc/pretix.cfg so you can test pretix out of the box
* We set django debuf to false at ./etc/pretix.cfg to avoid css erros 

### Tested menus

Admin session

* Dashboard
* Events
* Organizers
* Create new organizer
* Order search
* User settings
* Create user
* Global settings

Organizer session

* Events
* Settings
* Teams
* Create new team
* Devices
* Gift Cards
* Webhooks

### Helper commands

* `./bin/prodserver.sh` to start nginx/gunicorn via supervisor
* `./bin/stopprodserver.sh` to stop nginx/gunicorn via supervisor
* `./bin/runserver.sh` to start django runserver
* `./bin/manage.sh` to access django management commands
* `./bin/logs.sh` to access django management commands
* `./bin/shell.sh` to access bash shell

### Pretix Notes:

* https://docs.pretix.eu/en/latest/admin/installation/docker_smallscale.html#next-steps
* https://docs.pretix.eu/en/latest/development/setup.html

### Contract Notes:

* https://medium.com/coinmonks/a-really-simple-smart-contract-on-how-to-insert-value-into-the-ethereum-blockchain-and-display-it-62c455610e98

### Pretix Dashboard

* Dashboard: `http://localhost:8000/control/`
* User: `admin@localhost`
* Password: `admin`

1. Create an organizer
2. Create an event
3. Start presales

### Todo:

##### Pretix environment setup

* Docker
* SMTP
* nginx (reverse proxy)
* PostgreSQL
* redis
* pretix application `docker pull pretix/standalone:stable`
* `pretix.cfg` for pulling it all together

##### Contract development

* create solidity smart contract to accept payment with order id
* store orderId and with payment
* enable contract creator to withdraw funds
* deploy to ganache testnet

##### API

* create standalone Flask application for POC, later migrate to Pretix(Django)
* manually register contract address and ABI with API
* provide contract ABI and address to client
* provide unique order ID to client
* provide ether conversion of order price to client
* receive posted transaction id so api can start listening for event
* on successful network confirmation update the associated Pretix Order

##### Client

* create standalone HTML5/JS/Web3/MetaMask payment page, later inject via Pretix template
* give MetaMask prompt if not found
* instantiate web3 and enable ethereum
* show order, with price in dollars and in ether
* show payment button
* when payment is made, pull up MetaMask and confirm (updated) price in ether
* once transaction is made, ping the API with the transaction ID

##### Pretix Integration

* create plugin `Etherpay`
* subclass `Etherpay` from `BasePaymentProvider` and fill in required info
* update required templates
* register `Etherpay` payment gateway with Pretix
* pray it works
* resolve all issues until it does

##### Caveats

* no refunds right now (manual, contact administrator)
* only one contract owner for withdrawals
* a single contract for every event -- later we can improve to handle multiple events, and multiple organizers.

### Process

1. Get Pretix docker-compose development environment up and running
1. Create dummy organization and event
1. Create Etherpay contract and deploy via Remix to testnet
1. Manually integrate contract address and ABI to API
1. Create Flask API and html5 webclient, pull all data from API
1. Test transactions on client
1. Test event discovery on API
1. Integrate with Application


