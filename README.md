# Simple Stock Management - Frontend Client Component

## Security Advisory

Please note, this application has not been audited for security and *probably does* contain vulnerabilities that could expose data contained on the host system to unauthorized manipulation or disclosure, both during the building process and deployment. Use at your own risk.

## About


The system allows "stores" to request transfers of stock ("order") from a central stock repository ("warehouse"). Stock is adjusted for the "Warehouse Account" and the "Store Account" as stock transfers are "ordered". Email notifications are sent to the "warehouse" administrator(s) and the ordering "store manager".

This project - available to subscribers and clients as a regularly maintained application-as-a-service - offers a web frontend that connects to a RESTful API backend. Data is stored in either a SQLite, mySQL or PostgreSQL (recommended) database.


## Key Technologies for Client Component

Key technologies include: Javascript (ReactJS); HTML5; CSS3; BootStrap 4.

## Live Demo

There is a live demo, available here:

https://frontend.ssm.webapps.uplandsdynamic.com

There are two test users - one for the warehouse administrator, the other for a 'store manager'. Credentials are:

Adminstrator:
Username: test_admin
Password: jduejHje(89K

Manager:
Username: test_manager
Password: jduejHje(89K

## Screenshots

![screenshot_1](https://github.com/12Aruna/simple-stock-management-in-frontend/assets/122152267/d7b45b35-5cd0-45cb-94d1-41f512ff255f)

![screenshot_2](https://github.com/12Aruna/simple-stock-management-in-frontend/assets/122152267/dee50bc6-b17f-4220-9bef-0662b7f644cf)

![screenshot_4](https://github.com/12Aruna/simple-stock-management-in-frontend/assets/122152267/88b0d89d-ef09-4888-934f-bf98a16682b5)

![screenshot_6](https://github.com/12Aruna/simple-stock-management-in-frontend/assets/122152267/e9fc9f28-eb75-45df-b1f1-4db24100ceee)

![screenshot_7](https://github.com/12Aruna/simple-stock-management-in-frontend/assets/122152267/8f497020-531e-4941-9f37-d8f2ecb0f515)


![screenshot_8](https://github.com/12Aruna/simple-stock-management-in-frontend/assets/122152267/431afe0f-5bea-4ac3-af91-026c39dc5ba8)

![screenshot_5](https://github.com/12Aruna/simple-stock-management-in-frontend/assets/122152267/c429deb9-3f14-48b7-b154-20813967eae3)









## Key features

- Administrator may add, edit and delete stock from database.
est transfers ("order") stock from the "warehouse".
- Dynamic search of stock lines (SKU and description).
- Configurable pagination of results table.
- Transfer requests of stock lines are loaded to a "truck" (i.e. like "adding to a basket/cart" in an e-commerce system), before the request is submitted.
  - The "truck" retains the transfer data until the "Request truck dispatch" button is clicked. The truck data is retained across sessions (meaning the data remains in the truck even if the user logs out, then resumes their transfer at a later time).
  - Once the "Request truck dispatch" button is clicked, the transfer request process will complete. The truck empties and a single email containing a summary of the successful transfers - and any failures - is dispatched to both the requesting user and the warehouse administrator. Warehouse quantities are immediately adjusted accordingly, both in the "Warehouse" and "Store" accounts.
- A "Stock take" feature compiles and emails detailed reports, consisting of:

  - For every unique stock line in a "Store Account" (see screenshot #10, below, for an example report):

    - SKU
    - Stock description
    - Units of opening stock
    - Units of closing stock
    - Change in stock units since last stock take
    - Number of units transferred since last stock take
    - Number of units recorded sold since last stock take
    - Number of units recorded as shrinkage since last stock take
    - Differential for units of unrecorded history since last stock take (i.e. unrecorded sales, unrecorded transfers, unrecorded loss)
    - Current transfer value of a unit
    - Current retail price of a unit
    - Total value of units recorded sold since last stock take
    - Total value of units recorded as shrinkage since last stock take
    - Total value of units transferred since last stock take
    - Total value differential of units with unrecorded history since last stock take, at present xfer price
    - Total value differential of units with unrecorded history since last stock take, at present retail price (i.e. unrecorded sales, unrecorded transfers, shrinkage)
    - Current total held stock transfer value at present xfer price
    - Current total held stock retail value at present retail price

  - Overview of the entire "Store Account" (see screenshot #10, below, for an example report):

    - Units of opening stock
    - Units of closing stock
    - Units of stock transferred since last stock take
    - Units of stock recorded sold since last stock take
    - Units of stock recorded as shrinkage since last stock take
    - Change in stock holding owing to unrecorded unit history since last stock take (i.e. unrecorded sales, unrecorded transfers, unrecorded loss)
    - Value of stock recorded sold since last stock take
    - Value of stock recorded as shrinkage since last stock take
    - Total value differential of units with unrecorded history since last stock take at current transfer value
    - Total value differential of units with unrecorded history since last stock take at current retail value (i.e. unrecorded sales, unrecorded transfers, unrecorded loss)
    - Total value of transfers since last stock take (at actual xfer prices)
    - All time total value of transfers (at actual xfer prices)
    - Value of held stock at current transfer price
    - Value of held stock at current retail price

- Automated removal of obsolete stock line records (lines with zero units of held stock) from the Store accounts following a successful stock take process
- Historical retention of previous stock take data (not currently exposed on the UI)

## Brief UI instructions

Warehouse administrators:

- Plus sign button allows adding new stock lines
- Circular arrows button refreshes records from the database
- Pencil icon button in `Action` column allows editing of stock line
- Dustbin icon button in `Action` column allows deletion of a stock line

Store account managers:

- Head-&-shoulders icon (right of top header bar) switches between `Warehouse` account (from where transfers are requested) and the user's `Store` account
- Truck icon (right of top header bar) opens the user's "transfer truck"
- Circular arrows button refreshes records from the database
- Plus sign button allows manual addition of new lines to the `Store` account
- Pencil icon button in `Action` column allows editing of stock line data (e.g. change stock level, record a sale or shrinkage, etc)
- `New shrinkage` & `New recorded sold` update fields are ***disabled** during a stock line edit if the `stock quantity` field is changed. This is to prevent user error by inadvertent duplication of submitted data (i.e. user manually decrementing the `stock quantity` field whilst also recording the same data as `New recorded sold`). Likewise, the `stock quantity` field is disabled if the `New shrinkage` and/or `New recorded sold` fields are edited, for the same reason
- Eye icon button initiates a stock take

## Installation & Usage (on Linux systems)

__Below are basic steps to install and run a demonstration of the app on an Linux Ubuntu 20.04 server. They do not provide for a secure installation, such as would be required if the app was publicly available. Steps should be taken to security harden the environment if using in production.__

### Brief Installation Instructions

- Clone repository to an app source directory of your choice, e.g. `git clone https://github.com/Aninstance/simple-stock-management-frontend.git`.
- Make web root directory, e.g. `mkdir -p /var/www/html/ssm-frontend`.
- Move into the cloned directory and install the required node packages. Ensure a current version of NPM is installed and active on your system - it's recommended to install NVM (Node Version Manager) - which allows multiple node versions to be installed - to avoid changing a pre-installed version that may be required by other software or packages on your system.
- Install npx on your system if not already installed, e.g.: `npm install -g npx`.
- Install the packages by running `npm install`.
- In the event of any vulnerabilities being flagged up, run `npm audit fix`.
- Configure the app environment by coping the `.env.production_DEFAULT` file to `.env.production` and editing according to your requirements.
- Build the app, e.g.: `npm run build:production`.
- Copy the built app into its web directory, e.g. `cp -a build/. /var/www/html/ssm-frontend/;` `cp -a /var/www/html/ssm-frontend/static. /var/www/html/ssm-frontend/;`.
- Recursively change ownership of the `ssm-frontend` directory to your web server user.
- Configure your web server to serve the app from your web directory (this is straight forward, but outwith the scope of this document. If you need further help, please check your web server's documentation).

### Update Instructions

- Ensure you backup a copy of changes to your environment configuration - make a copy of your `.env.production` file *outside* of your cloned directory.
- From the build directory, run `git pull`.
- Remove existing node modules, e.g.: `rm -rf node_modules`.
- Remove the package lock file, e.g.: `rm -rf package-lock.json`.
- Install updated modules, e.g.: `npm install`.
- In the event of any vulnerabilities being flagged up, run `npm audit fix`.
- Rebuild the project, e.g.: `npm run build:production`.
- Once the app has been built, copy to the web directory: `cp -a build/. /var/www/html/ssm-frontend/;` `cp -a /var/www/html/ssm-frontend/static/. /var/www/html/ssm-frontend/;`.
- Recursively change ownership of the `ssm-frontend` directory to your web server user.
- Restart your web server.

Note: The above guide is not definitive and is intended for users who know their way around Ubuntu server and Django.

*Users would need to arrange database backups and to secure the application appropriately when used in a production environment.*

## Development Roadmap

- No new features planned at present. To request a change or additional functionality, or to file a bug, please open a github issue and/or contact dan@uplandsdynamic.com.

