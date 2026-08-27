# 📖 Grimório 20 — Android

Aplicativo Android desenvolvido em **Java + Android Studio + WebView** para executar o **Grimório 20** como um aplicativo próprio no Android.

O projeto funciona como uma camada Android nativa que carrega a versão Web do Grimório 20 publicada no GitHub Pages.

<p align="center">
  <img src="https://img.shields.io/badge/Android-Studio-3DDC84?logo=androidstudio&logoColor=white" />
  <img src="https://img.shields.io/badge/Java-Android-orange?logo=openjdk&logoColor=white" />
  <img src="https://img.shields.io/badge/WebView-Android-3DDC84?logo=android&logoColor=white" />
  <img src="https://img.shields.io/badge/Expo-React%20Native-000020?logo=expo&logoColor=white" />
  <img src="https://img.shields.io/badge/GitHub-Pages-181717?logo=github&logoColor=white" />
</p>

---

## 🎯 Sobre o projeto

O **Grimório 20** é uma aplicação voltada para consulta e organização de magias de **Tormenta 20**.

Este repositório contém especificamente a versão Android construída no **Android Studio**, utilizando uma `WebView` para executar a interface Web do projeto principal.

A arquitetura foi separada em dois projetos:

```text
┌──────────────────────────────┐
│      Projeto-T20             │
│                              │
│ Expo + React Native          │
│ Catálogo de magias           │
│ Busca e filtros              │
│ AsyncStorage                 │
└──────────────┬───────────────┘
               │
               │ Expo Web
               ▼
┌──────────────────────────────┐
│       GitHub Pages           │
│                              │
│ Aplicação Web publicada      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│   Projeto-T20-Android        │
│                              │
│ Android Studio               │
│ Java                         │
│ WebView                      │
│ APK Android                  │
└──────────────────────────────┘
```

---

## 🌐 Projeto principal

O código principal do Grimório 20 está disponível em:

**[vbmelo-hub/Projeto-T20](https://github.com/vbmelo-hub/Projeto-T20)**

A aplicação Web utilizada pela WebView está publicada em:

**[Grimório 20 — GitHub Pages](https://vbmelo-hub.github.io/Projeto-T20/)**

---

## 📱 Como funciona

Ao iniciar o aplicativo Android:

```text
Grimorio20
    ↓
MainActivity.java
    ↓
WebView
    ↓
GitHub Pages
    ↓
Projeto-T20
    ↓
Grimório 20
```

A `MainActivity` configura a WebView para:

* habilitar JavaScript;
* habilitar DOM Storage;
* manter a navegação dentro do aplicativo;
* carregar o Grimório 20 através do GitHub Pages;
* utilizar o botão voltar do Android para retornar no histórico da WebView.

---

## 🛠️ Tecnologias utilizadas

### Aplicação Android

* Android Studio
* Java
* Android SDK
* Gradle
* WebView
* XML

### Aplicação carregada pela WebView

* Expo
* React Native
* React Native Web
* JavaScript
* AsyncStorage
* GitHub Pages

---

## 📂 Estrutura principal

```text
Projeto-T20-Android/
│
├── app/
│   └── src/
│       └── main/
│           │
│           ├── java/
│           │   └── com/example/grimorio20/
│           │       └── MainActivity.java
│           │
│           ├── res/
│           │   └── layout/
│           │       └── activity_main.xml
│           │
│           └── AndroidManifest.xml
│
├── gradle/
├── build.gradle.kts
├── settings.gradle.kts
├── gradlew
└── gradlew.bat
```

---

## 🧠 MainActivity

O núcleo do aplicativo Android está em:

```text
app/src/main/java/com/example/grimorio20/MainActivity.java
```

A WebView é configurada aproximadamente da seguinte maneira:

```java
webView = findViewById(R.id.webview);

webView.getSettings().setJavaScriptEnabled(true);
webView.getSettings().setDomStorageEnabled(true);

webView.setWebViewClient(new WebViewClient());

webView.loadUrl(
    "https://vbmelo-hub.github.io/Projeto-T20/"
);
```

O uso de:

```java
webView.setWebViewClient(new WebViewClient());
```

faz com que a navegação continue dentro da aplicação, evitando que as páginas sejam abertas automaticamente em um navegador externo.

---

## 🔐 Permissão de Internet

Como o conteúdo é carregado através do GitHub Pages, o aplicativo precisa de acesso à Internet.

No `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

---

## 💻 Como executar

### 1. Clone o repositório

```bash
git clone https://github.com/vbmelo-hub/Projeto-T20-Android.git
```

### 2. Abra no Android Studio

Abra a pasta:

```text
Projeto-T20-Android
```

e aguarde a sincronização do Gradle.

### 3. Escolha um dispositivo

Você pode executar em:

* emulador Android;
* smartphone físico com depuração USB habilitada.

### 4. Execute

No Android Studio:

```text
Run ▶ app
```

O Android Studio irá:

```text
Compilar
   ↓
Gerar APK
   ↓
Instalar
   ↓
Abrir Grimorio20
```

---

## 📦 Gerando um APK

No Android Studio:

```text
Build
→ Build App Bundle(s) / APK(s)
→ Build APK(s)
```

Após a compilação, o APK de debug normalmente estará em:

```text
app/build/outputs/apk/debug/app-debug.apk
```

Esse arquivo pode ser transferido para um dispositivo Android e instalado manualmente.

---

## 🔄 Atualização do conteúdo

Uma característica importante dessa arquitetura é que a interface principal não precisa ser recompilada toda vez que o Grimório recebe uma atualização.

O fluxo é:

```text
Alteração no Projeto-T20
          ↓
Build da versão Web
          ↓
Deploy no GitHub Pages
          ↓
WebView carrega a nova versão
          ↓
Aplicativo Android atualizado
```

Portanto, alterações no conteúdo e na interface Web podem ser disponibilizadas sem a necessidade de gerar um novo APK.

Um novo APK só é necessário quando houver alterações na camada Android propriamente dita.

---

## ⚠️ Dependência de Internet

Esta versão do aplicativo utiliza uma **WebView online**.

A aplicação Web é hospedada no GitHub Pages. A primeira carga normalmente depende de conexão com a Internet. Após os recursos serem carregados, a WebView pode reutilizar arquivos em cache, permitindo que o aplicativo continue funcionando offline em determinadas situações. Os dados do usuário são armazenados localmente com AsyncStorage. O funcionamento offline após limpeza dos dados ou em uma instalação nova não é garantido.

---

## 🎓 Contexto acadêmico

Este projeto foi desenvolvido como aplicação de conceitos de **desenvolvimento híbrido para dispositivos móveis**, combinando:

```text
Android nativo
      +
Java
      +
WebView
      +
Aplicação Web
      +
React Native / Expo
```

A proposta demonstra a integração entre uma aplicação Web multiplataforma e uma camada Android construída diretamente no Android Studio.

---

## 🔗 Repositórios

| Projeto             | Tecnologia               | Repositório                                                              |
| ------------------- | ------------------------ | ------------------------------------------------------------------------ |
| Grimório 20         | Expo / React Native      | [Projeto-T20](https://github.com/vbmelo-hub/Projeto-T20)                 |
| Grimório 20 Android | Java / Android / WebView | [Projeto-T20-Android](https://github.com/vbmelo-hub/Projeto-T20-Android) |

---

## 👨‍💻 Desenvolvimento

Desenvolvido por **[@vbmelo-hub](https://github.com/vbmelo-hub)**.

---

<p align="center">
  <strong>📖 Grimório 20</strong><br>
  Magias, personagens e organização para Tormenta 20.
</p>
