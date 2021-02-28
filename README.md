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

## Cálculo experiência próximo nível

Baseado em como os RPG calculam: logarítmo ou potência

const experienceToNextLevel = Math.pow((level + 1) \* 4, 2);

level + 1 -> próximo level

4 é o fator de experiência (mais fácil ou mais difícil)

## Estrutura básica de context

```

import { createContext, ReactNode } from "react";

interface CountdownContextData {

}

interface CountdownProviderProps {
  children: ReactNode;
}

const CountdownContext = createContext({} as CountdownContextData);

export function CountdownProvider({ children }: CountdownProviderProps) {

  return (
    <CountdownContext.Provider value={{}}>
      {children}
    </CountdownContext.Provider>
  );
}

```

## Definição de provider

Não deve ir por "fora" se houver uma dependência.

E a hierarquia deve respeitar quem usa o contexto de quem.

No caso, **Countdown** usa o contexto do **Challenges**

\_app.tsx

```

<ChallengesProvider>
  <CountdownProvider>
    <Component {...pageProps} />
  </CountdownProvider>
</ChallengesProvider>
```

No entanto, CountdownProvider não é usada em toda a app (logo, não precisa estar em \_app.tsx)

Colocamos em torno de onde será utilizado (na home: **index.tsx**):

```

<CountdownProvider>
    <section>
      <div>
        <Profile />
        <CompletedChallenges />
        <Countdown />
      </div>
      <div>
        <ChallengeBox />
      </div>
    </section>
</CountdownProvider>
```

E então remove do \_app.tsx

```

<ChallengesProvider>
  <Component {...pageProps} />
</ChallengesProvider>


-> ChallengesProvider passou para index.tsx quando foi utilizado cookies

```

## Storage

- Local Storage: armazena sempre em texto no formato chave, valor

- Session Storage: similar ao Local Storage, mas só existe durante a sessão

- IndexedDB: banco de dados mais completo

- WebSQL: não está disponível em todos os browsers, é similar a um sqlite da vida

- Cookies: similar ao Local Storage, permite definir que um cookie é disponível em um domínio ou mais (local storage é só para um domínio), permite definer quando expira, definir cookie HttpOnly (acessível na camada backend ou fronted - se for true, não consegue acessar diretamente do js no frontend), definir se é Secure (só quando a aplicação tem https), SameSite (cookie disponível no site com o mesmo domínio)

Next.js geralmente usa Cookies para armazenamento de preferências do usuário por exemplo, pois está disponível em todas as camadas da aplicação (backend, frontend, camada intermediária - serviço do Next.js)
A menos que seja uma informação que só precisa estar disponível na camada visual (browser - Local Storage é específico do browser)

### Biblioteca para salvar cookie

```shell

1. Instalar biblioteca para salvar cookie

  yarn add js-cookie

Adicionar tipagem do js-cookie (foi construída com js e não typescript - aparece três pontinhos quando faz import) a partir de um repositório

  Como localizar tipagens disponíveis:

  a. Em https://www.npmjs.com/package/@types/react é possível encontrar informações de como instalar, inclusive o repositório das tipagens https://github.com/DefinitelyTyped/DefinitelyTyped#readme

  b. Clicar na pasta "types"

2. Instalar tipagem do js-cookie como dependência de desenvolvimento

  yarn add @types/js-cookie -D
```

Salvando nos Cookies

```
  useEffect(() => {
    Cookies.set("level", String(level));
    Cookies.set("currentExperience", String(currentExperience));
    Cookies.set("challengesCompleted", String(challengesCompleted));
  }, [level, currentExperience, challengesCompleted]);

```

-> Não esquecer de dar refresh na aba de cookies quando estiver visualizando no navegador

## getServerSideProps

Só funciona nas "pages", não funciona em outros componentes

```

// Executa no servidor node e não no navegador
// Ex.: se tiver algum log.console, vai aparecer no terminal do node e não no console do navegador

// Resolve problema de SEO (o motor de busca não espera a página buscar tudo para indexar)
// Implementando no getServerSideProps, as informações são carregadas antes,
// resolvendo este problema de SEO

// Deve ter este nome getServerSideProps obrigatoriamente e
// deve ser async, mesmo que não faça chamada assíncrona

export const getServerSideProps: GetServerSideProps = async (ctx) => {
  const { level, currentExperience, challengesCompleted } = ctx.req.cookies;

  return {
    props: { level, currentExperience, challengesCompleted },
  };
};

```

## Demo

Hospedado no Netlify. Para acessar, clique [aqui](https://vigilant-mirzakhani-cf915c.netlify.app)

## Referências

- [Notificação Web](https://developer.mozilla.org/pt-BR/docs/Web/API/Notification)
- [Áudio](https://developer.mozilla.org/en-US/docs/Web/API/HTMLAudioElement/Audio)
