# move.it-Next

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

## Arquivo \_document.tsx

Carrega uma única vez

Colocar tudo que é estático, que se mantém em todas as telas

O \_app.tsx é reaproveitado, porém recalculado a cada página acessada (gera processamento a mais).

## CSS Modules

CSS limitado a apenas para um componente. Exemplo ExperienceBar.module.css

## Imagem Github

```
<img src="https://github.com/nomeusuario.png"/>
```

## Escrever condicional sem else

```

{hasFinished ? <p>Terminou...</p> : null}

OU

{hasFinished && <p>Terminou2...</p>}

```

## Fragment

```
<></>

```

## Hack em css

```
.challengeActive footer button:hover {
  filter: brightness(0.9);
}
```

## Tópicos de estudo CSS

- Grid

- Flexbox

## Context Api

Fornece uma maneira de passar os dados entre os componentes

Antes resolvia só com Redux

## Definir tipo no Typescript

type ou interface

children?: -> campo opcional

children: -> campo obrigatório

## Cálculo experiência

Baseado em como os RPG calculam

logarítmo ou potência

const experienceToNextLevel = Math.pow((level + 1) \* 4, 2);

level + 1 -> próximo level

4 é o fator de experiência (mais fácil ou mais difícil)

## Demo

Hospedado no Netlify. Para acessar, clique [aqui](https://vigilant-mirzakhani-cf915c.netlify.app)

## Referências
