## Partie 1 - Dockerisation du front (5 points)

### Fichier Dockerfile crée dans la racine du front

```bash
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install     

COPY . .

EXPOSE 5001

CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0", "--port", "5001"]
```
Difficulté lors dulancement du build initilement je souhaite le lancer avec ce model de Dockerfile : 
```bash
FROM node:20-alpine

WORKDIR /app

RUN npm i -g serve

COPY package.json package-lock.json* ./
RUN npm install

COPY . .
RUN npm run build

EXPOSE 5001
CMD ["serve", "-s", "dist", "-p", "5001"]
```
Mais cela n'a pas fonctionné 

### Commande pour creer l'image 
```bash
docker build -t sabsab38/front-dev .
```
### Commande pour run l'image
```bash
docker run --rm -p 5001:5001 sabsab38/front-dev
```

## Dockerisation du back

### Fichier Dockerfile crée dans la racine du back

```bash
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "dist/index.js"]
```

### Commande pour creer l'image 
```bash
docker build -t sabsab38/back-dev .
```
### Commande pour run l'image
```bash
docker run --rm -p 1992:3000 sabsab38/back-dev
```


## Mise en production

