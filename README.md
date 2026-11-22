# Campo Minado — Android (HTML + GitHub Actions)

Este projeto empacota o seu `index.html` enviado em um aplicativo Android usando Capacitor. O GitHub Actions compila o APK automaticamente e publica o arquivo em **Releases** quando você envia uma tag `v*`.

## O que já está configurado

- Aplicativo: **Campo Minado**
- Identificador Android: `br.com.campominado.app`
- Seu jogo HTML original está em `www/index.html`.
- Compilação automática pelo GitHub Actions.
- Publicação automática no GitHub Releases ao enviar uma tag, por exemplo `v1.0.0`.

## Publicar no GitHub

1. Crie um repositório no GitHub, por exemplo `campo-minado-android`.
2. Envie o conteúdo desta pasta para a branch `main` (os arquivos e pastas, não o ZIP fechado).
3. Abra a aba **Actions** do repositório. Se solicitado, habilite workflows.
4. Para testar a compilação, selecione **Compilar APK e publicar no GitHub Releases** e clique em **Run workflow**.
5. Quando terminar, abra a execução e baixe `Campo-Minado-APK` em **Artifacts**.

## Fazer um lançamento

Depois que o projeto estiver na branch `main`, crie e envie uma tag:

```bash
git tag v1.0.0
git push origin v1.0.0
```

Isso inicia uma nova compilação e cria um lançamento em **Releases**, anexando `app-debug.apk`.

Para uma atualização futura, envie suas alterações e use uma tag nova, como `v1.0.1`. Não reutilize uma tag já publicada.

## Atualizar o jogo

Substitua `www/index.html` pela nova versão do seu HTML. Mantenha `appId` igual em `capacitor.config.json` para que o Android reconheça o aplicativo como o mesmo app.

## Aviso importante: APK de teste e assinatura de produção

A configuração atual gera `app-debug.apk`, assinado com a chave de depuração automática. É apropriado para testar o fluxo e instalar manualmente, mas não é a configuração recomendada para distribuir atualizações de produção.

Antes de distribuir amplamente, configure uma chave de assinatura de produção (keystore) e os segredos necessários no GitHub Actions. Guarde a keystore e as senhas fora do repositório e faça backup seguro. Todas as versões futuras precisam usar a mesma chave e o mesmo `appId`; caso contrário, o Android pode impedir a atualização por cima da instalação existente.

## Personalização futura

- Nome exibido: `appName` em `capacitor.config.json`.
- Identificador do pacote: `appId` em `capacitor.config.json`.
- Jogo: `www/index.html`.

## Tecnologias

- HTML, CSS e JavaScript
- Capacitor 6
- GitHub Actions
- Android Gradle Plugin / Java 17

Documentação: https://capacitorjs.com/docs


## Ícone do aplicativo

O ícone realista está em `assets/icon.png`. Durante a compilação automática, o workflow gera os ícones Android para diferentes densidades e o ícone adaptativo. Para trocar o ícone futuramente, substitua `assets/icon.png` por outra imagem quadrada de alta resolução, mantendo o mesmo caminho e nome.


## Correção da geração do ícone

O workflow configura Python e Pillow, cria a pasta Android, gera os ícones (PNG e adaptativos) e só então sincroniza e compila o projeto. O arquivo `scripts/generate-icons.py` precisa permanecer no repositório junto de `assets/icon.png`.
