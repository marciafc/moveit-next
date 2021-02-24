# moveit-next

Aplicação com Next.js

## Criar projeto

```shell
yarn create next-app moveit-next

OU

npx create-next-app moveit-next

```

Renomear \_app.js para \_app.tsx

- Tudo que é global, que se repete em todas as páginas, fica no \_app.tsx

Renomear index.js para index.tsx

Instalar typescript, tipagens da biblioteca React, tipagens da biblioteca React dom, depend Node, tudo como dependência de desenvolvimento

```shell
$ yarn add typescript @types/react @types/react-dom @types/node -D
```

## Start na aplicação

```shell
$ yarn dev

localhost:3000

```

## Javascript

Se desabilitar o javascript no settings do navegador, continua funcionando (veio do intermediário - servidor do Next.js)

## Migrar projeto moveit para moveit-next

Organizar estrutura similar a do projeto moveit, criado anteriormente e copiar arquivos/trechos.

Reiniciar a aplicação yarn dev

## Demo

Hospedado no Netlify. Para acessar, clique [aqui]()

## Referências
