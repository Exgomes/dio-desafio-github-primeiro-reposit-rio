git [-v | --versão] [-h | --help] [-C <caminho>] [-c <nome>=<valor>]

​      [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]

​      [-p | --paginar | -P | --no-pager] [--no-replace-objects] [--bare]

​      [--git-dir=<caminho>] [--work-tree=<caminho>] [--namespace=<nome>]

​      [--super-prefix=<caminho>] [--config-env=<nome>=<envvar>]

​      <comando> [<args>]

Estes são comandos comuns do Git usados em várias situações:

iniciar uma área de trabalho (veja também: git help tutorial)

  clone Clone um repositório em um novo diretório

  init Cria um repositório Git vazio ou reinicializa um existente

trabalhe na mudança atual (veja também: git help todos os dias)

  add Adiciona o conteúdo do arquivo ao índice

  mv Move ou renomeia um arquivo, um diretório ou um link simbólico

  restaurar Restaurar arquivos da árvore de trabalho

  rm Remove arquivos da árvore de trabalho e do índice

examine o histórico e o estado (veja também: revisões do git help)

  bisect Use a busca binária para encontrar o commit que introduziu um bug

  diff Mostra as mudanças entre commits, commit e árvore de trabalho, etc

  grep Imprime linhas que correspondem a um padrão

  log Mostrar logs de commit

  show Mostra vários tipos de objetos

  status Mostra o status da árvore de trabalho

crescer, marcar e ajustar sua história comum

  branch Listar, criar ou excluir branches

  commit Grava as alterações no repositório

  merge Junte dois ou mais históricos de desenvolvimento

  rebase Reaplicar commits em cima de outra dica base

  reset Restaura o HEAD atual para o estado especificado

  mudar Mudar ramos

  tag Criar, listar, excluir ou verificar um objeto de tag assinado com GPG



colaborar (veja também: git help workflows)

  buscar Baixar objetos e referências de outro repositório

  puxar Busca de e integrar com outro repositório ou uma ramificação local

  push Atualizar referências remotas junto com objetos associados



'git help -a' e 'git help -g' listam os subcomandos disponíveis e alguns

guias de conceito. Veja 'git help <comando>' ou 'git help <conceito>'

para ler sobre um subcomando ou conceito específico.

Veja 'git help git' para uma visão geral do sistema.—————————————————————————————————————————-

GITTUTORIAL(7) Manual do Git GITTUTORIAL(7)

NOME

​    gittutorial - Um tutorial de introdução ao Git

SINOPSE

​    git *

DESCRIÇÃO

​    Este tutorial explica como importar um novo projeto para o Git, fazer alterações

​    a ele e compartilhe as alterações com outros desenvolvedores.

​    Se você estiver interessado principalmente em usar o Git para buscar um projeto,

​    por exemplo, para testar a versão mais recente, você pode preferir começar com o

​    primeiros dois capítulos do Manual do Usuário do Git[1].

​    Primeiro, observe que você pode obter a documentação de um comando como git log

​    --grafo com:

​      $man git-log

​    ou:

​      $ git log de ajuda

​    Com este último, você pode usar o visualizador de manuais de sua escolha; veja git-

​    help(1) para mais informações.

​    É uma boa ideia se apresentar ao Git com seu nome e público

​    endereço de e-mail antes de fazer qualquer operação. A maneira mais fácil de fazer isso é:

​      $ git config --global user.name "Seu nome vem aqui"

​      $ git config --global user.email you@yourdomain.example.com

IMPORTANDO UM NOVO PROJETO

​    Suponha que você tenha um tarball project.tar.gz com seu trabalho inicial. Você pode

​    coloque-o sob o controle de revisão do Git da seguinte maneira.

​      $ tar xzf project.tar.gz

​      projeto $ cd

​      $ git init

​    Git irá responder

  Repositório Git vazio inicializado em .git/

 Você agora inicializou o diretório de trabalho - você pode notar um novo

 diretório criado, chamado ".git".

Em seguida, diga ao Git para tirar um instantâneo do conteúdo de todos os arquivos sob o diretório atual (observe o .), com git add:

 $git adicionar.

​    Este instantâneo agora está armazenado em uma área de teste temporária que o Git chama

​    o índice". Você pode armazenar permanentemente o conteúdo do índice no

​    repositório com git commit:

​      $ git commit

​    Isso solicitará uma mensagem de confirmação. Agora você armazenou o primeiro

​    versão do seu projeto no Git.

FAZENDO MUDANÇAS

​    Modifique alguns arquivos e adicione seu conteúdo atualizado ao índice:

​      $ git adicionar arquivo1 arquivo2 arquivo3

​    Agora você está pronto para se comprometer. Você pode ver o que está prestes a ser cometido

​    usando git diff com a opção --cached:

​      $ git diff --cache

​    (Sem --cached, git diff mostrará todas as alterações que você fez

​    mas ainda não adicionado ao índice.) Você também pode obter um breve resumo do

​    situação com status do git:

​    $ git status

​      No mestre do ramo

​      Alterações a serem confirmadas:

​      Seu branch está atualizado com 'origin/master'.

​       (use "git restore --staged <file>..." para desfazer o stage)

​          modificado: arquivo1

​          modificado: arquivo2

​          modificado: arquivo3



​    Se você precisar fazer outros ajustes, faça-o agora e, em seguida, adicione qualquer

​    conteúdo recém-modificado para o índice. Por fim, confirme suas alterações com:

​      $ git commit

​    Isso solicitará novamente uma mensagem descrevendo a alteração e, em seguida,

​    gravar uma nova versão do projeto.

​    Como alternativa, em vez de executar git add de antemão, você pode usar

​      $ git commit -a

​    que notará automaticamente quaisquer arquivos modificados (mas não novos), adicione

​    para o índice e confirme, tudo em uma única etapa.

​    Uma observação sobre mensagens de confirmação: embora não seja obrigatório, é uma boa ideia começar

​    a mensagem de confirmação com uma única linha curta (menos de 50 caracteres) resumindo a alteração, seguida por uma linha em branco e, em seguida, uma linha mais completa

​    Descrição. O texto até a primeira linha em branco em uma mensagem de confirmação é

​    tratado como o título do commit, e esse título é usado em todo o Git. Por

​    Por exemplo, git-format-patch(1) transforma um commit em email e usa o

​    título na linha Assunto e o resto do commit no corpo.

GIT TRACKS CONTEÚDO NÃO ARQUIVOS

​    Muitos sistemas de controle de revisão fornecem um comando add que informa ao

​    sistema para iniciar o rastreamento de alterações em um novo arquivo. O comando add do Git faz

​    algo mais simples e poderoso: git add é usado tanto para novos

​    arquivos recém-modificados e, em ambos os casos, tira um instantâneo do dado

​    arquivos e encena esse conteúdo no índice, pronto para inclusão no

​    próximo compromisso.

VISUALIZANDO O HISTÓRICO DO PROJETO

​    A qualquer momento você pode ver o histórico de suas alterações usando

​      $ git log

​    Se você também quiser ver diferenças completas em cada etapa, use

​      $ git log -p

​    Muitas vezes, a visão geral da mudança é útil para ter uma ideia de cada etapa

​     $ git log --stat --summary

GESTÃO DE FILIAIS

​    Um único repositório Git pode manter várias ramificações de desenvolvimento. Para

​    crie um novo branch chamado "experimental", use

​      $ git branch experimental

​    Se você agora correr

​      $ git branch

​    você obterá uma lista de todas as ramificações existentes:

​       experimental

\* mestre

​    O branch "experimental" é aquele que você acabou de criar, e o "master"

​    branch é um branch padrão que foi criado para você automaticamente. o

​    o asterisco marca a ramificação em que você está atualmente; modelo

​      $ git switch experimental

​    para mudar para o ramo experimental. Agora edite um arquivo, confirme a alteração,

​    e volte para o branch master:

​      (editar arquivo)

​      $ git commit -a

​      $ git switch master

​    Verifique se a alteração que você fez não está mais visível, pois foi feita em

​    o branch experimental e você está de volta ao branch master.

​    Você pode fazer uma alteração diferente no branch master:

​      (editar arquivo)

​      $ git commit -a

​    neste ponto os dois ramos divergiram, com diferentes mudanças feitas

​    em cada. Para mesclar as alterações feitas no experimental no master, execute

​      $ git merge experimental

​    Se as alterações não entrarem em conflito, está feito. Se houver conflitos,

​    marcadores serão deixados nos arquivos problemáticos mostrando o conflito;

​      $ git diff

​    vai mostrar isso. Depois de editar os arquivos para resolver os conflitos,

​      $ git commit -a

​    confirmará o resultado da mesclagem. Finalmente,

​      $ gitk

​    irá mostrar uma bela representação gráfica do histórico resultante.

​    Neste ponto, você pode excluir o branch experimental com

​      $ git branch -d experimental

​    Este comando garante que as mudanças no branch experimental sejam

​    já na filial atual.

​    Se você desenvolver em uma ideia maluca do ramo, então se arrependa, você sempre pode

​    excluir o ramo com

$ git branch -D ideia maluca

​    As filiais são baratas e fáceis, então esta é uma boa maneira de experimentar algo.

USANDO O GIT PARA COLABORAÇÃO

​    Suponha que Alice tenha iniciado um novo projeto com um repositório Git em

​    /home/alice/project, e aquele Bob, que tem um diretório home no mesmo

​    máquina, quer contribuir.

​    Bob começa com:

​      bob$ git clone /home/alice/project myrepo

​    Isso cria um novo diretório "myrepo" contendo um clone do arquivo de Alice

​    repositório. O clone está em pé de igualdade com o projeto original,

​    possuir sua própria cópia da história do projeto original.

​    Bob então faz algumas alterações e as confirma:

​      (editar arquivos)

​      bob$ git commit -a

​      (repita conforme necessário)

​    Quando estiver pronto, ele diz a Alice para extrair as alterações do repositório em

​    /home/bob/myrepo. Ela faz isso com:

​      alice$ cd /home/alice/projeto

​      alice$ git pull /home/bob/myrepo master

​    Isso mescla as alterações da ramificação "mestre" de Bob na ramificação atual de Alice.

​    ramo. Se Alice fez suas próprias mudanças nesse meio tempo, então ela pode

​    precisa corrigir manualmente quaisquer conflitos.

​    O comando "pull" realiza assim duas operações: busca as alterações

​    uma ramificação remota e, em seguida, mescla-os na ramificação atual.

​    Observe que, em geral, Alice gostaria que suas alterações locais fossem confirmadas antes

​    iniciando este "puxão". Se o trabalho de Bob entrar em conflito com o que Alice fez desde

​    suas histórias bifurcadas, Alice usará sua árvore de trabalho e o índice para

​    resolver conflitos, e as mudanças locais existentes irão interferir no

​    processo de resolução de conflitos (o Git ainda executará a busca, mas

​    recusar-se a mesclar — Alice terá que se livrar de suas alterações locais em alguns

​    caminho e puxe novamente quando isso acontecer).

​    Alice pode espiar o que Bob fez sem mesclar primeiro, usando o comando "buscar"

​    comando; isso permite que Alice inspecione o que Bob fez, usando um

​    símbolo "FETCH_HEAD", para determinar se ele tem algo que valha a pena

​    puxando, assim:

​      alice$ git fetch /home/bob/myrepo master

​      alice$ git log -p HEAD..FETCH_HEAD

Essa operação é segura mesmo se Alice tiver alterações locais não confirmadas. o

​    notação de intervalo "HEAD..FETCH_HEAD" significa "mostrar tudo o que é

​    alcançável a partir do FETCH_HEAD, mas exclua qualquer coisa alcançável a partir

​    CABEÇA". Alice já sabe tudo o que leva ao seu estado atual

​    (HEAD) e revisa o que Bob tem em seu estado (FETCH_HEAD) que ela tem

​    não visto com este comando.

​    Se Alice quiser visualizar o que Bob fez desde que suas histórias se bifurcaram, ela

​    pode emitir o seguinte comando:

​      $ gitk HEAD..FETCH_HEAD

​    Isso usa a mesma notação de intervalo de dois pontos que vimos anteriormente com o git log.

​    Alice pode querer ver o que os dois fizeram desde que se bifurcaram. Ela pode

​    use a forma de três pontos em vez da forma de dois pontos:

​      $ gitk HEAD...FETCH_HEAD

​    Isso significa "mostrar tudo o que é alcançável de qualquer um, mas

​    excluir qualquer coisa que seja alcançável de ambos".

​    Observe que esta notação de intervalo pode ser usada com gitk e "git

​    registro”.

Depois de inspecionar o que Bob fez, se não houver nada urgente, Alice pode

​    decidir continuar trabalhando sem puxar de Bob. Se a história de Bob

​    tiver algo que Alice precisaria imediatamente, Alice pode optar por

​    esconda seu trabalho em andamento primeiro, faça um "puxão" e, finalmente, desmonte

​    seu trabalho em andamento em cima da história resultante.

​    Quando você está trabalhando em um pequeno grupo muito unido, não é incomum

​    interagir com o mesmo repositório repetidamente. Ao definir remoto

​    abreviação de repositório, você pode facilitar:

​      alice$ git remote add bob /home/bob/myrepo

​    Com isso, Alice pode realizar a primeira parte da operação de "puxar" sozinha

​    usando o comando git fetch sem mesclá-los com seu próprio branch,

​    usando:

​      alice$ git buscar bob

​    Ao contrário do formulário à mão, quando Alice busca de Bob usando um controle remoto

​    repositório abreviado configurado com git remote, o que foi buscado é armazenado

​    em um branch de rastreamento remoto, neste caso bob/master. Então depois disso:

​      alice$ git log -p master..bob/master

​    mostra uma lista de todas as mudanças que Bob fez desde que ele ramificou de

​    Ramo mestre de Alice.

​    Depois de examinar essas alterações, Alice pode mesclar as alterações em seu

​    ramo mestre:

​      alice$ git mesclar bob/master

​    Essa mesclagem também pode ser feita puxando de seu próprio rastreamento remoto

​    ramo, assim:

​      alice$ git pull . controles remotos/bob/master

​    Observe que o git pull sempre se funde com o branch atual, independentemente de

​    o que mais é dado na linha de comando.

​    Mais tarde, Bob pode atualizar seu repositório com as últimas alterações de Alice usando

​      bob$ git pull

​    Observe que ele não precisa fornecer o caminho para o repositório de Alice; quando

​    Bob clonou o repositório de Alice, Git armazenou a localização do repositório dela

​    na configuração do repositório, e esse local é usado para pulls:

​      bob$ git config --get remote.origin.url

​      /home/alice/projeto

(A configuração completa criada pelo git clone é visível usando git

​    config -l, e a página man git-config(1) explica o significado de cada

​    opção.)

​    O Git também mantém uma cópia original do branch master de Alice sob o nome

​    "origem/mestre":

​      bob$ git branch -r

​       origem/mestre

​    Se Bob decidir mais tarde trabalhar em um host diferente, ele ainda poderá realizar

​    clona e puxa usando o protocolo ssh:

​      bob$ git clone alice.org:/home/alice/project myrepo

​    Alternativamente, o Git tem um protocolo nativo ou pode usar http; veja git-

​    pull(1) para detalhes.

​    O Git também pode ser usado no modo CVS, com um repositório central que

​    vários usuários enviam alterações; veja git-push(1) e gitcvs-migration(7).

EXPLORANDO A HISTÓRIA

​    O histórico do Git é representado como uma série de commits inter-relacionados. Nós temos

​    já vi que o comando git log pode listar esses commits. Observe que

​    a primeira linha de cada entrada do git log também dá um nome para o commit:

​      $ git log

​      confirmar c82a22c39cbc32576f64f5c6b3f24b99ea8149c7

​      Autor: Junio C Hamano <junkio@cox.net>

​      Data: Ter, 16 de maio 17:18:22 2006 -0700

​        merge-base: Esclareça os comentários sobre o pós-processamento.

​    Podemos dar este nome ao git show para ver os detalhes deste commit.

​      $ git show c82a22c39cbc32576f64f5c6b3f24b99ea8149c7

​    Mas existem outras maneiras de se referir a commits. Você pode usar qualquer inicial

​    parte do nome que é longa o suficiente para identificar exclusivamente o commit:

​      $ git show c82a22c39c # os primeiros caracteres do nome são

​                  \# geralmente o suficiente

​      $ git show HEAD # a ponta do branch atual

​      $ git show experimental # a ponta do branch "experimental"

​    Cada commit geralmente tem um commit "pai" que aponta para o anterior

​    estado do projeto:

​      $ git show HEAD^ # para ver o pai de HEAD

​      $ git show HEAD^^ # para ver o avô de HEAD

​      $ git show HEAD~4 # para ver o tataravô de HEAD

Observe que os commits de mesclagem podem ter mais de um pai:

​      $ git show HEAD^1 # mostra o primeiro pai de HEAD (o mesmo que HEAD^)

​      $ git show HEAD^2 # mostra o segundo pai de HEAD

​    Você também pode dar seus próprios nomes aos commits; depois de correr

​      $ git tag v2.5 1b2e1d63ff

​    você pode se referir a 1b2e1d63ff pelo nome "v2.5". Se você pretende compartilhar

​    esse nome com outras pessoas (por exemplo, para identificar uma versão de lançamento),

​    você deve criar um objeto "tag", e talvez assiná-lo; veja git-tag(1) para

​    detalhes.

​    Qualquer comando Git que precise conhecer um commit pode receber qualquer um desses nomes.

​    Por exemplo:

​      $ git diff v2.5 HEAD # compara o HEAD atual com a v2.5

​      $ git branch stable v2.5 # inicia um novo branch chamado "stable" baseado

​                  \# na v2.5

​      $ git reset --hard HEAD^ # redefine seu branch atual e está funcionando

​                  \# diretório para seu estado em HEAD^

​    Cuidado com esse último comando: além de perder qualquer alteração no

​    o diretório de trabalho, ele também removerá todos os commits posteriores deste

​    ramo. Se esta ramificação for a única ramificação que contém esses commits, eles

​    será perdido. Além disso, não use git reset em uma ramificação publicamente visível que

​    outros desenvolvedores extraem, pois forçará fusões desnecessárias em outros

​    desenvolvedores para limpar o histórico. Se você precisar desfazer as alterações que você

​    tenha empurrado, use git revert em vez disso.

​    O comando git grep pode pesquisar strings em qualquer versão do seu

​    projeto, então

​      $ git grep "olá" v2.5

​    procura por todas as ocorrências de "hello" na v2.5.

​    Se você deixar de fora o nome do commit, o git grep pesquisará qualquer um dos arquivos

​    ele gerencia em seu diretório atual. Então

​      $ git grep "olá"

​    é uma maneira rápida de pesquisar apenas os arquivos rastreados pelo Git.

​    Muitos comandos Git também aceitam conjuntos de commits, que podem ser especificados em um

​    número de maneiras. Aqui estão alguns exemplos com git log:

​      $ git log v2.5..v2.6 # commits entre v2.5 e v2.6

​      $ git log v2.5.. # commits desde a v2.5

​      $ git log --since="2 semanas atrás" # commits das últimas 2 semanas

​      $ git log v2.5.. Makefile # commits desde a v2.5 que modificam

\# Makefile

Você também pode dar ao git log um "intervalo" de commits onde o primeiro não é

​    necessariamente um ancestral do segundo; por exemplo, se as pontas do

​    branches "stable" e "master" divergiram de um commit comum algum tempo

​    atrás, então

​      $ git log estável..master

​    irá listar os commits feitos no branch master mas não no branch estável,

​    enquanto

​      $ git log master..stable

​    mostrará a lista de commits feitos no branch estável, mas não o

​    ramo mestre.

​    O comando git log tem um ponto fraco: ele deve apresentar commits em uma lista.

​    Quando a história tem linhas de desenvolvimento que divergiram e depois se fundiram

​    novamente, a ordem na qual o git log apresenta esses commits é

​    sem significado.

​    A maioria dos projetos com vários contribuidores (como o kernel Linux ou

​    Git em si) têm merges frequentes, e o gitk faz um trabalho melhor de

​    visualizando sua história. Por exemplo,

​      $ gitk --since="2 semanas atrás" drivers/

​    permite que você navegue por qualquer commit das últimas 2 semanas de commits que

​    arquivos modificados no diretório "drivers". (Nota: você pode ajustar

​    fontes do gitk mantendo pressionada a tecla control enquanto pressiona "-" ou "+".)

​    Finalmente, a maioria dos comandos que aceitam nomes de arquivos, opcionalmente, permitem que você

​    preceder qualquer nome de arquivo por um commit, para especificar uma versão específica do

​    Arquivo:

​      $ git diff v2.5:Makefile HEAD:Makefile.in

​    Você também pode usar git show para ver qualquer arquivo desse tipo:

​      $ git show v2.5:Makefile

PRÓXIMOS PASSOS

​    Este tutorial deve ser suficiente para realizar a revisão distribuída básica

​    controle de seus projetos. No entanto, para compreender completamente a profundidade e

​    poder do Git, você precisa entender duas ideias simples sobre as quais é

​    Sediada:

​    • O banco de dados de objetos é o sistema bastante elegante usado para armazenar os

​      histórico do seu projeto—arquivos, diretórios e commits.

• O arquivo de índice é um cache do estado de uma árvore de diretórios, usado para

​      crie commits, verifique os diretórios de trabalho e mantenha os vários

​      árvores envolvidas em uma fusão.

​    A segunda parte deste tutorial explica o banco de dados de objetos, o arquivo de índice,

​    e algumas outras probabilidades e pontas que você precisará para aproveitar ao máximo o Git.

​    Você pode encontrá-lo em gittutorial-2(7).

​    Se você não quiser continuar com isso imediatamente, alguns outros

​    as digressões que podem ser interessantes neste momento são:

​    • git-format-patch(1), git-am(1): Estes convertem séries de commits git

​      em patches enviados por e-mail e vice-versa, útil para projetos como o

​      Kernel Linux que depende muito de patches enviados por e-mail.

​    • git-bisect(1): Quando há uma regressão em seu projeto, uma forma de

​      rastrear o bug é pesquisando no histórico para encontrar o

​      commit exato que é o culpado. O Git bisect pode ajudá-lo a realizar um

​      busca binária para esse commit. É inteligente o suficiente para realizar um

​      busca próxima do ideal mesmo no caso de complexos não lineares

​      histórico com muitas ramificações mescladas.

​    • gitworkflows(7): Fornece uma visão geral dos fluxos de trabalho recomendados.

​    • giteveryday(7): Git diário com 20 comandos ou mais.

​    • gitcvs-migration(7): Git para usuários CVS.

VEJA TAMBÉM

​    gittutorial-2(7), gitcvs-migration(7), gitcore-tutorial(7),

​    gitglossary(7), git-help(1), gitworkflows(7), giteveryday(7), O Git

​    Manual do usuário[1]

GIT

​    Parte do pacote git(1)

NOTAS

​    \1. O Manual do Usuário do Git

​      git-htmldocs/user-manual.html

Git 2.37.0 27/06/2022 GITTUTORIAL(7)

(FIM)