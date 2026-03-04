# MANUAL DO GAME COMPANION (PT-BR)

**V 1.4.2 - Mar/2026**

O aplicativo Game Companion funciona como um gerenciador de ambiente de jogo personalizado que permite gerenciar bibliotecas de jogos e automatizar o ambiente pré e pós-jogo. Ele foi testado no Windows 10 e Windows 11.

O Game Companion permite configurar uma biblioteca de utilitários — como opentrack, trackir, joystick gremlin, drivers de volante ou joystick, crewchief, SRS, dial exporters, etc. — bem como uma biblioteca de jogos locais ou da Steam. No cadastro de utilitários, é possível indicar se o utilitário deve ser lançado antes (trackir, crewchief, etc.) ou depois do jogo já estar em execução (ex: OBS), bem como informar seu método de fechamento (sinal gracioso, kill task ou comando com argumentos) após o término do jogo.

# Para quem é este aplicativo?

Usuários preguiçosos como eu, ou aqueles cansados de usar arquivos .bat ou .cmd para gerenciar utilitários (principalmente jogadores) que alternam entre diferentes softwares (geralmente jogos), que usam diferentes aplicações para configurar o ambiente antes do uso e desejam que o sistema seja "limpo" automaticamente após o uso.

# Instalação

Basta copiar tanto o `GameCompanion.exe` quanto o `runner.exe` para uma pasta. É melhor não utilizá-lo dentro de "Arquivos de Programas" ou outras pastas "monitoradas" do Windows, pois o Game Companion criará uma pasta de cache e arquivos de log nesta mesma pasta, e às vezes o Windows pode bloquear o acesso nestas pastas monitoradas específicas.

# Tela Principal - Biblioteca de Jogos

Esta é a aparência que seu Game Companion pode ter após você criar sua biblioteca de jogos. 
Na tela principal do Game Companion, você encontrará seus cartões de jogos. 
Para iniciar um jogo, basta clicar em um cartão. O Game Companion executará toda a sequência de início de utilitários, chamará seu jogo e, ao final dele, executará toda a sequência de parada definida naquele cartão. 
Para editar um cartão, clique no botão de edição no canto superior direito do cartão. 
Para alterar a ordem dos cartões, use as setas laterais em cada cartão para movê-lo na grade. 
A alteração de ordem só pode ser feita na categoria **ALL**, e as outras categorias herdam a ordem desta categoria principal automaticamente. Os botões aparecem quando você passa o mouse sobre os cartões.

- **Monitoramento de Status:** O app monitora se o jogo está "Iniciando", "Jogando" ou se houve um erro, exibindo esta informação em uma barra de status.
- **Prevenção de Conflitos:** O app não permite iniciar um segundo jogo enquanto um ainda estiver sendo monitorado.
- **Cancelamento de Inicialização:** Se um jogo demorar a responder, você pode cancelar o processo de lançamento diretamente pelo cartão.

#### Figura 1 - Tela principal
![Main](https://github.com/user-attachments/assets/a9012f5d-1618-47ae-886b-261950590b76)

# Registro de Utilitários

O primeiro passo é o registro de utilitários, feito pelo primeiro botão no canto superior esquerdo (aquele com um símbolo de ferramentas). Isso nos leva à tela abaixo, mostrada já preenchida com alguns utilitários para fins de exemplo.
#### Figura 2 - Tela de Registro de Utilitários
<p align="center">
  <img src="https://github.com/user-attachments/assets/bbab1904-2335-4d76-88b7-6e18d3723623" width="600">
</p>
![Utilities](https://github.com/user-attachments/assets/bbab1904-2335-4d76-88b7-6e18d3723623)

Preencher esta tela é simples: No lado esquerdo, há uma lista de utilitários já registrados e um botão X ao lado de cada nome para excluir o referido utilitário. Clicar no nome do utilitário entra no modo de edição (à direita). Para adicionar um utilitário, quando não estiver editando um, basta preencher os dados na tela da direita e pressionar o botão **SAVE**.

**Campos:**

- **Name:** (como você quer chamar este utilitário)
- **ID:** (deixe em branco ou especifique um nome diferente para distinguir de outra entrada com o mesmo nome de utilitário, se houver)
- **Executable Path:** (indique onde o utilitário está no seu disco)
- **Arguments:** (indique quaisquer argumentos de chamada, separados por espaço)
- **Post-launch wait (ms):** tempo de espera até chamar o próximo utilitário da fila ou o jogo
- **Instant:** (marque se este utilitário se fecha sozinho após ser chamado e não depende do Game Companion para ser fechado)
- **Delay:** (marque se o utilitário deve ser chamado apenas após o jogo já estar em execução)
- **Run as Admin:** se você precisar rodar como admin apenas para um jogo específico, em vez de marcar o utilitário para rodar como admin no Windows, você pode marcar aqui (você pode até criar dois perfis para o mesmo utilitário, com e sem permissões de admin)
- **Stop Method:** escolha entre 3 formas:
  - **Signal:** (O Windows envia um sinal de fechamento ao utilitário)
  - **Kill:** (O Windows mata a tarefa do utilitário) <- método garantido
  - **Command:** (chama o utilitário novamente passando argumentos definidos)

**NOTA:** O método de fechamento mais garantido, embora o menos elegante, é o Force Kill. Teste seus utilitários; se eles aceitarem o método Signal, dê preferência a este. Se eles tiverem um método que utiliza argumentos, dê preferência ao Command. Use Force Kill como último recurso.

# Gerenciamento da Biblioteca de Jogos

O Game Companion permite centralizar seus jogos em uma interface visual organizada por "cartões". Para fazer isso, após ter registrado alguns utilitários, acesse o segundo botão no topo direito da tela (aquele com um símbolo de controle). Isso abrirá a seguinte tela: 
#### Figura 3 - Tela de registro de jogos
<p align="center">
  <img src="https://github.com/user-attachments/assets/5e6079b5-0bf5-4ea1-a8b8-614d25b8471d" width="600">
</p>
Para o registro de jogos, temos dois métodos:

### Via Steam

Se o seu jogo for da Steam, ou se você quiser aproveitar uma imagem legal de jogo vinda da biblioteca Steam, comece digitando o nome do jogo no primeiro campo (Import from Steam). Selecione o jogo na lista que aparecerá, e a tela será autopreenchida com o caminho `steam://` do jogo e sua imagem. Se o jogo já estiver instalado na sua máquina, o aplicativo tentará localizar seu executável mais provável e preencher o campo "Process Name".

Note que alguns jogos, como ARMA 3 ou AUTOMOBILISTA 2, possuem mais de um executável possível, e o aplicativo pode escolher um que não seja o ideal. Verifique sempre para garantir que o nome do processo seja de fato o que seu jogo utiliza quando executado. (ex: no ARMA 3, geralmente é `arma3_x64.exe`, e no AMS2 é geralmente `AMS2AVX.exe`).

Alguns jogos, quando lançados usando o protocolo `steam://`, especialmente aqueles baseados na Madness Engine, podem apresentar dificuldades para trabalhar com Opentrack ou Trackir (ou qualquer software que injete algo na memória compartilhada). Esta é uma limitação que não consegui superar. Se você encontrar tais casos, certifique-se de registrar o jogo usando o "método de instalação local" (abaixo) em vez do protocolo "steam://".

### Via instalação local

Caso queira registrar um jogo que não seja da Steam, ou se apenas usou a busca da Steam como forma de popular rapidamente a imagem para o cartão do jogo, preencha os outros campos de nome, caminho e processo com as informações apropriadas. Nota: Quando você indica um jogo que não é da Steam, o aplicativo busca extrair o ícone do jogo para representá-lo no cartão no momento de salvar, a menos que você forneça explicitamente uma imagem.  
Lembre-se: o processo é geralmente o nome do arquivo executável do jogo. Você \*deve\* incluir a extensão nele (geralmente .exe).

O campo **timeout** determina quantos segundos o Game Companion deve esperar para detectar o processo do jogo na memória antes de julgar que o lançamento não foi bem-sucedido. Normalmente a detecção é feita em menos de um segundo após o início do jogo, mas para casos em que o jogo é acionado a partir de um "launcher" (ex: ARMA 3, Assetto Corsa via Content Manager ou DCS), você pode querer colocar um tempo maior para permitir que o launcher carregue, mudar algo nele e só então executar o jogo em si. Dica: se possível, se o seu jogo tiver um launcher, configure o launcher para permanecer na memória após chamar o jogo; desta forma, você pode indicar o processo do launcher para ser monitorado em vez do jogo em si. Isso é mais interessante do que monitorar o jogo diretamente, evitando o caso de fechar o jogo e retornar ao launcher apenas para configurar outra sessão e ter o processo de "fechamento de jogo" chamado, encerrando todos os utilitários que foram abertos antes do jogo.

Você também tem um tempo de **"wait"** (espera, em ms!) que é o tempo que o Game Companion espera para chamar utilitários atrasados após o início do jogo. Padrão=0.

Os jogos podem ser atribuídos a uma ou mais categorias. As categorias são definidas nas opções gerais do Game Companion. Mais sobre isso depois.

### Sequência de Inicialização e Sequência de Parada

Aqui é onde a mágica acontece. À esquerda temos a lista da Sequência de Início (**Start Sequence**), e à direita temos a lista da Sequência de Parada (**Stop Sequence**). No lado esquerdo, você marca os utilitários que deseja executar antes do jogo quando clicar no seu cartão de jogo. Note que eles aparecerão na ordem inversa na lista da direita (em vermelho), que é a ordem de execução para fechamento após o jogo terminar. Você pode alterar as ordens de início e fim desmarcando e marcando novamente na ordem desejada em ambas as listas. Deixar um utilitário desmarcado em qualquer lista indica ao Game Companion que aquele utilitário deve ser ignorado ao processar a referida lista. Ex: se você marcou um utilitário para iniciar deixando-o azul na lista da esquerda, mas não quer que o Game Companion o feche ao final do jogo, você pode marcar este utilitário como "Instant" no seu registro de utilitário, ou alternativamente simplesmente desmarcá-lo da lista da direita (Stop Sequence) no registro de um jogo específico. Se não estiver marcado em vermelho, ele será ignorado durante a sequência de fechamento.

**NOTA: Sempre que vir um campo com o símbolo ⓘ ao lado do rótulo, passe o mouse sobre ele para ver uma ajuda rápida.**

# Customização e Configurações Globais

O usuário pode ajustar a aparência e o comportamento do Game Companion usando o terceiro botão no topo da janela (aquele com o símbolo de uma engrenagem), que abrirá a seguinte janela:
#### Figura 4 - Tela de configurações globais
<p align="center">
  <img src="https://github.com/user-attachments/assets/3372248e-9d25-4be0-be20-792bc5a8b4a2" width="600">
</p>
- **Card Size:** Permite ajustar o tamanho da grade de jogos (pequeno, médio ou grande) para melhor visibilidade.
- **Background Modes:** Suporta fundo com gradiente dinâmico ou o uso de papel de parede personalizado. Um papel de parede padrão acompanha o Game Companion, mas você pode escolher outro se preferir.
- **Categories:** Permite a criação de categorias para classificação dos jogos. Cada jogo pode participar de mais de uma categoria. Todos os jogos participam da categoria **ALL** obrigatoriamente.
- **Default Tab:** Define qual categoria deve ser exibida assim que o aplicativo for aberto.
- **Auto Close:** Se marcado, fará o Game Companion fechar após a sessão de jogo ser finalizada.
- **Enable Debug:** gera um arquivo `app.log` na mesma pasta do Game Companion, onde as mensagens das atividades realizadas pelo aplicativo são armazenadas para verificação de seu funcionamento. A cada nova sessão, o log é sobrescrito.  
    Você pode ler o log (se houver) pressionando o botão "View Log".

# NOTAS GERAIS SOBRE O GAME COMPANION

**O Game Companion foi desenvolvido em Go + Wails. Ele usa algumas técnicas que podem causar falsos positivos no antivírus, como varreduras de registro e disco (para procurar a localização da Steam e dos jogos Steam) e chamadas a bibliotecas do Windows para extração de ícones (quando o usuário não determina uma imagem para o jogo). Além disso, as várias chamadas de biblioteca para rodar e fechar (em 3 formas diferentes!) apps e jogos frequentemente disparam falsos positivos, especialmente quando estão todos empacotados em um utilitário tão pequeno.**

**Sistema de Cache e Performance**

- **Otimização de Imagem:** Todas as imagens de capa são redimensionadas e convertidas internamente para garantir que a interface permaneça rápida e consuma pouca memória.
- **Persistência Automática:** Qualquer alteração em jogos, utilitários ou configurações é salva automaticamente em um arquivo `config.json` de forma atômica para evitar perda de dados.
- **Chamadas a utilitários e jogos:** São feitas usando um launcher destacado que morre após a chamada, evitando que o Windows os classifique como "filhos" do Game Companion.
- **Rastreamento de Jogo:** Feito de forma muito leve e eficiente, usando as próprias chamadas do Windows que não sobrecarregam a CPU.
- **Cache de Imagem:** imagens de jogos e papel de parede são mantidos e gerenciados na pasta **CACHE**, dentro da pasta onde o Game Companion está instalado. As técnicas de redimensionamento e cópia para estas imagens são feitas para evitar sua transferência através da memória (stream), tornando o consumo de RAM o mais mínimo possível.

**Simplicidade:**

- O Game Companion armazena todas as configurações em um arquivo `config.json` na mesma pasta de onde o app é executado. Você pode editar o arquivo se desejar (por exemplo, se quiser excluir um grande bloco de jogos e/ou utilitários de uma só vez), mas certifique-se de saber o que está fazendo.

**O Game Companion foi projetado para ajudar o jogador com o uso mínimo de CPU, DISCO e RAM.**

## AVISO LEGAL (DISCLAIMER)

O desenvolvedor não é responsável por qualquer dano, incluindo, mas não se limitando a: perda de dados, falha de hardware, combustão espontânea ou invocação acidental de horrores sobrenaturais.

Se o seu PC começar a levitar ou emitir um leve cheiro de enxofre, consulte um padre, não a página de issues do GitHub, que, a propósito, nem sequer existe. Pelo lado positivo, este software tem a garantia de fazer algo. Se este "algo" é o que você esperava, ou um colapso digital completo, isso é uma questão inteiramente entre você e sua CPU. Ao usar este software, você renuncia completa e irrevogavelmente ao seu direito de reclamar, mesmo que o aplicativo decida se identificar como uma torradeira e se recuse a funcionar até que você insira pão.

Divirta-se. 

JoKeR_BR

# Em relação a possíveis falsos positivos (AV)

Se você enviar o GameCompanion ou seu `runner.exe` para o VirusTotal ou outros serviços de análise, descobrirá que alguns antivírus podem citá-lo como suspeito.

Exemplo de um item de análise feito pela Hybrid Analysis (<https://hybrid-analysis.com/>) que "assusta" muitos antivírus por aí:
![VT](https://github.com/user-attachments/assets/bd20bf7c-4b63-4be3-9835-ebbd8a4983e5)

Esta mensagem é um **clássico falso positivo** de ferramentas de análise estática (como CrowdStrike ou VirusTotal). Aqui está a explicação técnica de por que isso acontece:

1. **Onde o Game Companion usa "Criptografia"?**

O Game Companion NÃO usa criptografia para ofuscar o código, mas usa a **advapi32.dll** por dois motivos legítimos e necessários:

- **Registro do Windows:** O `runner.exe`, que é responsável por chamar e fechar apps e jogos de uma forma que não seja vinculada ao app principal, usa o pacote de registro para descobrir onde a Steam está instalada. No Windows, todas as funções de acesso ao registro (como `RegOpenKeyEx`) estão dentro da `advapi32.dll`.
- **Geração de Números Aleatórios:** O Wails (e pacotes como `google/uuid` que ele usa) precisa gerar IDs únicos quando um jogo é registrado. Em Go, isso chama o pacote `crypto/rand`, que no Windows usa funções da `advapi32.dll` (como `CryptGenRandom`) para garantir que os números sejam realmente aleatórios e seguros.

2. **Por que o alerta diz "para ofuscação"?**

Antivírus usam heurísticas: eles sabem que malwares usam a `advapi32.dll` para criptografar seus próprios dados e se esconder (ofuscação). Como o Game Companion é um "editor desconhecido" e usa esta DLL, o robô do antivírus assume o "pior cenário" (uso para ofuscação) em vez do "cenário real" (uso para ler o registro ou gerar um ID).

3. **E quanto ao "Microsoft.CognitiveServices.Speech.core.dll"?**

Existe uma explicação simples: Esta DLL **não faz parte do Game Companion**. O que acontece é que o analisador estático de antivírus possui um banco de dados de "assinaturas de comportamento". Ele está dizendo: *"Eu vi este padrão de chamadas da advapi32.dll no seu app, e este padrão é idêntico ao que vi em um componente oficial da Microsoft (Speech Core)."*

Ou seja, ele está comparando o comportamento do Game Companion com o de um componente de voz da Microsoft para tentar classificar o que o Game Companion está fazendo. **É uma comparação, não uma dependência.**

### Resumo

- **Uso de Criptografia:** Não, o Go usa os componentes de segurança do Windows (advapi32) apenas para ler o Registro e gerar IDs aleatórios.
- **Ofuscação:** Não existe nenhuma. É apenas uma suposição do robô analisador.
- **Risco:** Zero. É um comportamento padrão de qualquer aplicação Go/Wails que interage com o sistema.

Como mencionado na nota do manual, o Game Companion executa várias operações de arquivo e busca que o tornam suspeito para analisadores de código, mas ele não faz nada além de chamar e fechar aplicativos e jogos. Este é outro motivo pelo qual apps independentes em Go sofrem com falsos positivos: o runtime do Go faz chamadas de sistema que os programas antivírus consideram "profundas demais" para um app simples. Em caso de dúvida, basta executá-lo dentro de uma sandbox e veja por si mesmo.

Saudações,

**JoKeR_BR**
