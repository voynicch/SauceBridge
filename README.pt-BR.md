<div align="center">

<img src="assets/app_icon.png" width="128" alt="Ícone do SauceBridge">

# SauceBridge

### Gerenciador Windows de extensões para readers Android compatíveis com Mihon/Tachiyomi

Gerencie repositórios de extensões, instale e atualize APKs de fontes, detecte readers compatíveis, mantenha o Android Platform-Tools atualizado e conecte todo o ecossistema através de uma interface desktop baseada em ADB.

<br>

[![Versão](https://img.shields.io/badge/versão-1.0.1-4C8BF5?style=for-the-badge)](#)
[![Plataforma](https://img.shields.io/badge/Windows-10%20%2F%2011-0078D4?style=for-the-badge&logo=windows11&logoColor=white)](#)
[![Android](https://img.shields.io/badge/ADB-Platform--Tools-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#)
[![Criador](https://img.shields.io/badge/Criado%20por-WBCS-7C3AED?style=for-the-badge)](#)

[English](README.md) · **Português (Brasil)**

</div>

---

## O que é o SauceBridge?

**SauceBridge** é um aplicativo desktop para Windows que gerencia extensões APK de readers Android através do ADB.

Ele nasceu para centralizar um fluxo que normalmente fica espalhado entre vários lugares: extensões, repositórios, readers, atualizações e ferramentas ADB.

Em vez de baixar APKs manualmente, procurar URLs de repositórios, conferir versões dos readers e manter o Platform-Tools separadamente, o SauceBridge reúne tudo em uma única interface.

> **Um aplicativo desktop. Vários readers. Vários repositórios. Um único fluxo de extensões.**

---

## Por que usar o SauceBridge?

O ecossistema de extensões Mihon/Tachiyomi é poderoso, mas sua manutenção manual pode se tornar repetitiva.

O SauceBridge automatiza justamente as partes em que uma ferramenta determinística é mais confiável:

- **Agregação de repositórios** — carrega vários catálogos compatíveis ao mesmo tempo.
- **Deduplicação por package** — evita substituir cegamente o mesmo pacote Android entre repositórios.
- **Estado real via ADB** — versões instaladas vêm diretamente do aparelho conectado.
- **Detecção de readers** — identifica apps conhecidos e forks compatíveis.
- **Bridge de repositórios** — envia URLs de repositórios aos readers que aceitam deep links compatíveis.
- **Platform-Tools portátil** — gerencia ADB sem exigir Android Studio.
- **Diagnóstico e recuperação** — logs persistentes, backup das configurações, relatório de crash e diagnóstico portátil.

---

## Principais recursos

| Recurso | Função |
|---|---|
| **Instalar** | Instala extensões APK diretamente no Android conectado |
| **Atualizar** | Detecta extensões instaladas com versão mais nova no repositório |
| **Desinstalar** | Remove extensões instaladas no dispositivo |
| **Operações em lote** | Instala vários APKs usando o modo multi-package do ADB |
| **Múltiplos repositórios** | Mescla vários catálogos compatíveis |
| **Repos PT-BR** | Inclui presets voltados a fontes em português do Brasil |
| **Reader Manager** | Detecta Mihon, Komikku, Aniyomi, DropSauce e forks |
| **Bridge de repositórios** | Envia URLs compatíveis aos readers detectados |
| **Updates dos readers** | Verifica a release mais recente de readers conhecidos |
| **Platform-Tools Manager** | Instala, atualiza, reinstala ou usa um ADB externo |
| **Cache offline** | Usa catálogos em cache quando um repositório fica indisponível |
| **Busca avançada** | Busca por nome, package, fonte, site, idioma ou repositório |
| **Diagnóstico persistente** | Logs rotativos, crash report, recuperação de settings e relatório |

---

## Readers e famílias compatíveis

O SauceBridge possui lógica de detecção para readers e forks do ecossistema Mihon/Tachiyomi, incluindo:

| Reader / família | Extensões | Bridge de repositório |
|---|---:|---:|
| **Mihon** | APK | `tachiyomi://` quando suportado |
| **Komikku** | APK | `tachiyomi://` |
| **TachiyomiJ2K** | APK | `tachiyomi://` |
| **TachiyomiSY** | APK | `tachiyomi://` |
| **TachiyomiAZ** | APK | `tachiyomi://` |
| **Aniyomi** | Manga / anime APK | `aniyomi://` / fallback compatível |
| **Animiru** | APK compatíveis | fluxo de deep link compatível |
| **Nekoyomi** | Repositórios de extensões | fluxo compatível |
| **Reikai / Yōkai** | APK compatíveis | fluxo compatível |
| **Blueth Yokai** | APK compatíveis | fluxo compatível |
| **DropSauce** | Mihon APK / formatos relacionados | fallback manual seguro |
| **Tachiyomi legado** | APK legado | compatibilidade legada |

Forks desconhecidos que anunciem um handler `tachiyomi://` ou `aniyomi://` compatível também podem ser detectados automaticamente.

> APKs de extensões são filtrados explicitamente e nunca aparecem como se fossem readers.

---

## Biblioteca de repositórios integrada

O SauceBridge já inclui uma biblioteca de repositórios para evitar que o usuário tenha que procurar URLs manualmente.

Entre os presets estão:

- Keiyoushi
- Yūzōnō
- Cursed Yūzōnō
- FelipeGFA · PT-BR
- Project Nox · PT-BR
- Mihon Nexus · PT-BR
- MHExtensions
- presets filtrados e legados opcionais

Cada repositório pode ser ativado, desativado, reordenado, editado ou adicionado manualmente.

### Conflitos de package

Quando mais de um repositório oferece o mesmo Android package, o SauceBridge respeita a prioridade dos repositórios em vez de substituir automaticamente o APK apenas porque outra entrada possui `versionCode` maior.

Isso reduz a possibilidade de conflito de assinatura Android entre forks.

---

## Início rápido

1. Baixe o ZIP portátil mais recente em **Releases**.
2. Extraia a pasta `SauceBridge`.
3. Abra `SauceBridge.exe`.
4. Conecte o Android via USB.
5. Ative a **Depuração USB** e autorize o computador no aparelho.
6. Se necessário, abra **Platform-Tools** no SauceBridge e instale o ADB gerenciado.
7. Escolha as extensões desejadas e instale.

> O SauceBridge é portátil. Não é necessário instalar Python.

---

## Estrutura portátil
---

## Estrutura portátil

Dados graváveis ficam ao lado do executável:

```text
SauceBridge/
├── SauceBridge.exe
├── settings.json
├── settings.json.bak
├── cache/
├── diagnostics/
├── logs/
├── platform-tools/
├── profiles/
└── _internal/
```

Assets somente-leitura são carregados a partir do diretório de recursos do PyInstaller.

---

## Gerenciamento do Platform-Tools

O SauceBridge pode gerenciar sua própria cópia do Android Platform-Tools.

Ações disponíveis:

- verificar atualização;
- instalar;
- atualizar;
- reinstalar;
- usar o ADB gerenciado;
- selecionar um `adb.exe` externo;
- abrir a pasta do Platform-Tools;
- abrir as notas oficiais.

A verificação automática nunca instala atualizações sem confirmação.

Instalações externas de ADB nunca são sobrescritas.

---

## Segurança e confiabilidade

O SauceBridge evita automações frágeis sempre que possível.

### Repositórios nos readers

Quando o reader oferece um deep link compatível, o SauceBridge envia a URL pelo sistema de intents do Android e deixa o próprio app confirmar a inclusão.

Quando não existe um deep link público confiável, o fluxo passa a ser:

```text
Copiar URL → Abrir reader → Usuário confirma manualmente
```

O SauceBridge não modifica diretamente bancos privados dos readers.

### Configurações

`settings.json` é salvo de forma atômica e recebe backup automático.

Se o arquivo ficar inválido:

```text
settings.json
        ↓
settings.corrupt-AAAAMMDD-HHMMSS.json
        ↓
configurações seguras
```

O programa continua iniciando normalmente e registra a recuperação no log.

---

## Diagnóstico

O SauceBridge possui várias camadas de diagnóstico:

```text
logs/SauceBridge.log
saucebridge-crash.log
diagnostics/diagnostic-*.txt
run-debug.bat
```

O relatório pode incluir:

- versão do SauceBridge;
- informações do Windows e Python;
- versão do ADB / Platform-Tools;
- estado do dispositivo;
- repositórios ativos;
- extensões carregadas;
- extensões instaladas;
- atualizações disponíveis;
- readers detectados;
- informações do cache;
- caminhos utilizados pelo runtime.

---

## Estrutura do projeto

```text
SauceBridge/
├── assets/
│   ├── app_icon.ico
│   ├── app_icon.png
│   └── creator_signature.png
│
├── core/
│   ├── adb.py
│   ├── cache.py
│   ├── models.py
│   ├── platform_tools.py
│   ├── readers.py
│   ├── repo.py
│   ├── repositories.py
│   └── runtime.py
│
├── main.py
├── preflight.py
├── SauceBridge.spec
├── requirements.txt
├── build.bat
├── run.bat
├── run-debug.bat
├── PORTABLE.txt
└── README.md
```

---

## Princípios do projeto

### O estado do dispositivo é a fonte principal

Sempre que possível, informações de packages e versões vêm do Android via ADB.

### Repositórios devem ser previsíveis

Prioridade e conflitos de packages são tratados de forma explícita.

### Ferramentas externas continuam substituíveis

O usuário pode usar o Platform-Tools gerenciado ou escolher o próprio `adb.exe`.

### Os dados privados dos readers permanecem privados

O SauceBridge prefere intents públicos e interfaces documentadas em vez de editar bancos internos.

### Portátil significa portátil

Dados do programa permanecem na pasta do aplicativo e podem ser facilmente copiados, inspecionados ou apagados.

---

## Roadmap pós-1.0

Próximas versões podem explorar:

- perfis de readers mais detalhados;
- novos formatos de repositório;
- novos provedores de atualização;
- atualização opcional dos APKs dos readers com validação de assinatura;
- verificação de saúde dos repositórios;
- relatórios de compatibilidade;
- localização da interface.

---

## Contribuindo

Issues, testes, relatos de compatibilidade e Pull Requests serão bem-vindos quando o repositório público estiver disponível.

Ao relatar um problema, inclua o relatório de diagnóstico do SauceBridge sempre que possível.

Não publique arquivos pessoais, senhas, tokens, chaves de API ou outras informações privadas em uma issue.

---

## Aviso

SauceBridge é um projeto independente.

Não é um cliente oficial de Mihon, Tachiyomi, Aniyomi, Komikku, DropSauce ou dos repositórios listados pelo aplicativo.

Nomes e marcas de terceiros pertencem aos seus respectivos proprietários.

O SauceBridge apenas gerencia metadados de repositórios, pacotes de extensões, integração com readers e operações ADB escolhidas pelo usuário.

---

<div align="center">

<img src="assets/creator_signature.png" width="220" alt="Assinatura WBCS">

### Criado por WBCS

**SauceBridge · Ponte Windows ↔ Android para extensões**

</div>
