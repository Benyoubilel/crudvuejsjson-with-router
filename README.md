info:

vuejs 3

npm version: 8.13.1

nodejs version: 16.15.1


Installation

1)Clone the repo
```sh
git clone https://github.com/Benyoubilel/tp2-vuejs-jsondb.git
```
2)cd to repository

3)Install NPM packages
```sh
npm install
```
4)install json-server
```sh
npm install -g json-server
```
5)install vuelidate
```sh
npm install @vuelidate/core @vuelidate/validators
```
6) Create a db.json file with some data
7)
  ```sh
{
  "user": [
    {
       "id": "1"    
      "nom": "x",
      "prenom": "xy",
      "email": "x@gmail.com"
    }
    {
      "id": "2"    
      "nom": "z",
      "prenom": "xy",
      "email": "z@gmail.com"
    }
  ]
}
```
8)Start JSON Server
```sh
json-server --watch db.json
```
9)Start vue
```sh
npm run dev
```