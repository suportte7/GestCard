# GestCard 2.0 --- Guia do usuário e notas de atualização

**Objetivo deste documento:** explicar o que muda quando o GestCard 1.3
é atualizado para a versão 2.0, como cada ferramenta funciona e quais
cuidados devem ser tomados.

> **Atenção:** este guia descreve os recursos encontrados no pacote
> GestCard 2.0. A atualização do aplicativo web não atualiza
> automaticamente o Google Apps Script. Os testes de sincronização com o
> Google e de instalação real no Android não foram executados. Faça
> backup antes de atualizar.

------------------------------------------------------------------------

## 1. O que é o GestCard 2.0?

O GestCard 2.0 mantém a estrutura principal de cadastro e controle do
GestCard e acrescenta ferramentas de acompanhamento mensal, recuperação
de exclusões, relatórios, permissões locais e diagnóstico.

A versão 2.0 foi preparada para manter o banco de dados existente no
formato v4. A atualização acrescenta campos auxiliares; não foi
programada para apagar ou renomear os campos antigos. Mesmo assim, **é
obrigatório fazer um backup JSON completo antes da atualização**.

## 2. O que continua funcionando da versão anterior?

A versão 2.0 mantém os fluxos principais já existentes no aplicativo,
incluindo:

-   cadastro e gerenciamento de pessoas;
-   cadastro e configuração de cartões, com dias de fechamento e
    vencimento;
-   lançamento de compras e despesas;
-   divisão de compras entre pessoas;
-   lançamento de recebimentos e abatimentos;
-   cadastro e acompanhamento de acordos/parcelamentos;
-   edição de lançamentos;
-   visão geral e consultas por pessoa ou cartão;
-   calculadora rápida;
-   anexos de comprovantes, quando disponíveis no aparelho;
-   backup, importação e sincronização conforme a configuração atual do
    serviço.

A atualização não deve ser tratada como uma substituição do sistema por
outro. É uma evolução da aplicação que já existe. As funções financeiras
centrais foram mantidas no código, mas isso não equivale a um teste de
todos os dados reais do usuário.

## 3. Ferramentas novas ou ampliadas na versão 2.0

### 3.1 Painel financeiro mensal

**O que faz:** apresenta um resumo do mês de referência selecionado.

Mostra: - total de compras/despesas atribuídas ao mês de referência; -
total de recebimentos atribuídos ao mês de referência; - diferença entre
compras e recebimentos; - quantidade de movimentações consideradas.

**Como usar:** 1. Abra a área de visão geral/relatórios. 2. Escolha o
mês no campo "Mês de referência". 3. Toque em "Atualizar". 4. Confira os
totais apresentados.

**Como interpretar:** a diferença é calculada como compras menos
recebimentos. Ela é um resumo do fluxo registrado naquele mês, não uma
confirmação automática de dívida individual nem um extrato bancário.

### 3.2 Comparativo com o mês anterior

**O que faz:** compara os totais de compras e recebimentos do mês
escolhido com os do mês imediatamente anterior, usando barras para
facilitar a leitura.

**Como usar:** selecione o mês e atualize o painel. O comparativo é
atualizado junto com o resumo.

**Atenção:** o comparativo depende dos meses de referência cadastrados
nos lançamentos. Se uma compra ou recebimento estiver com mês de
referência incorreto, o comparativo também ficará incorreto.

### 3.3 Fechamento mensal

**O que faz:** grava uma fotografia dos totais de compras, recebimentos
e diferença do mês selecionado, junto com a data e o usuário que
realizou o fechamento.

**Como usar:** 1. Selecione o mês. 2. Confira os totais do painel. 3.
Toque em "Fechar mês selecionado". 4. Leia os valores apresentados e
confirme somente se estiverem corretos.

**O que acontece depois:** se os lançamentos forem alterados depois do
fechamento, o sistema compara os totais atuais com a fotografia salva e
sinaliza divergência.

**Reabrir:** a reabertura é uma ação administrativa. O registro de
reabertura é mantido no histórico.

**Limite importante:** fechamento mensal não bloqueia lançamentos, não
congela o mês e não substitui contabilidade formal. É um registro de
conferência dos totais naquele momento.

### 3.4 Painel de parcelas com vencimento estimado ultrapassado

**O que faz:** lista compras/parcelas cujo vencimento calculado pelo
sistema já passou, usando a referência da fatura e o dia de vencimento
configurado para o cartão.

Pode apresentar: - quantidade de parcelas com vencimento estimado
ultrapassado; - soma bruta dos valores listados; - pessoa, descrição,
cartão, mês de referência e data estimada de vencimento.

**Como usar:** abra o painel de parcelas/vencimentos na área de visão
geral e confira cada item.

**Atenção muito importante:** é uma estimativa baseada nas datas
cadastradas. O painel não comprova que a pessoa está devendo. Antes de
cobrar ou considerar um valor em atraso, confira pagamentos,
abatimentos, acordos, estornos e a configuração do cartão.

### 3.5 Central de notificações locais

**O que faz:** reúne alertas identificados no aparelho, como: - parcelas
com vencimento estimado ultrapassado; - parcelas com vencimento estimado
nos próximos sete dias; - alterações aguardando sincronização; -
ausência de ponto de restauração recente detectado no aparelho.

**Como usar:** consulte a central no painel financeiro.

**Limite:** esses avisos são verificações locais do aplicativo. Não são
confirmação do banco, da operadora do cartão ou do servidor. O alerta de
backup depende do registro local de ponto de restauração.

### 3.6 Lixeira inteligente para compras e recebimentos

**O que faz:** em vez de apagar imediatamente determinados lançamentos,
a versão 2.0 envia compras e recebimentos excluídos para uma lixeira
recuperável.

**Como usar para restaurar:** 1. Abra "Lixeira inteligente". 2. Localize
o registro. 3. Toque em "Restaurar". 4. Confirme a operação.

**Regra de segurança:** a restauração só é feita se o identificador
original estiver livre. Se já existir outro registro com o mesmo
identificador, o sistema cancela a restauração para evitar duplicidade.

**Apagar definitivamente:** essa ação exige administrador e não pode ser
desfeita.

**Limite:** a lixeira protege exclusões feitas a partir da versão 2.0.
Ela não recupera lançamentos que já tinham sido apagados antes da
atualização para a 2.0. A tela exibe até os 100 itens mais recentes.

### 3.7 Exportação de relatórios

A versão 2.0 acrescenta opções de exportação para facilitar análise e
arquivamento.

**CSV do mês selecionado** - Exporta compras e recebimentos do mês
escolhido. - Pode ser aberto no Excel ou em outros programas de
planilha.

**CSV do histórico completo** - Exporta os registros de compras e
recebimentos disponíveis no conjunto de dados carregado.

**Arquivo Excel (.xlsx)** - Gera uma pasta de trabalho com abas
"Compras", "Recebimentos" e "Resumo". - O resumo apresenta compras,
recebimentos e diferença do mês selecionado.

**Relatório PDF** - Monta um relatório do mês selecionado, com totais e
tabela de movimentações. - A geração usa a janela de impressão do
navegador; pode ser necessário permitir janelas e escolher "Salvar como
PDF".

**Qual formato usar?** - Para analisar dados em planilha: CSV ou XLSX. -
Para imprimir/compartilhar um resumo mensal: PDF. - Para restaurar o
sistema com seus dados: use o backup JSON, não CSV, XLSX ou PDF.

### 3.8 Permissões locais por usuário

**O que faz:** permite ao administrador confirmado configurar, para cada
usuário, quatro permissões na interface: - **Cadastrar:** permitir ou
bloquear novos cadastros; - **Editar:** permitir ou bloquear
alterações; - **Excluir:** permitir ou bloquear exclusões; -
**Receber:** permitir ou bloquear lançamentos de recebimentos.

**Como usar:** o administrador abre "Permissões locais por usuário" e
marca ou desmarca as opções de cada pessoa.

**Limite de segurança:** essas permissões são controles locais da
interface do aplicativo. Elas não substituem regras de autorização no
Google Apps Script nem garantem bloqueio no servidor. Se o usuário
acessar o serviço remoto por outro caminho, a validação precisa existir
também no backend. Portanto, não considere esse recurso uma segurança
completa de servidor.

### 3.9 Diagnóstico local e backup de segurança

**O que faz:** verifica informações técnicas do aparelho e da cópia
local, incluindo: - presença do banco local; - versão/formato do
banco; - schema auxiliar; - listas principais de compras e
recebimentos; - disponibilidade da lixeira e dos fechamentos; - suporte
do navegador a IndexedDB e Service Worker; - conexão com a internet; -
presença de endereço/configuração de nuvem; - quantidade de compras,
recebimentos, itens na lixeira e fechamentos; - tamanho aproximado do
banco; - horário de última verificação local de sincronização, quando
registrado.

**Como usar:** 1. Abra a seção de diagnóstico. 2. Toque em "Executar
diagnóstico". 3. Leia os itens marcados com ✓ ou ⚠. 4. Se necessário,
use "Baixar backup de segurança".

**O que o diagnóstico não faz:** não corrige automaticamente problemas,
não altera dados e não comprova que o servidor Google está íntegro ou
que outro aparelho recebeu os mesmos dados. Um resultado positivo de
conexão não garante sincronização concluída.

## 4. Estrutura de dados e preservação

A versão 2.0 mantém o banco de dados v4 e acrescenta três campos
auxiliares por conjunto de dados: - `gc20Lixeira`: registros enviados
para a lixeira; - `gc20Fechamentos`: fotografias dos fechamentos
mensais; - `gc20Preferencias`: preferências auxiliares da versão 2.0.

Quando esses campos não existem, a aplicação os inicializa. A intenção
da migração é aditiva: acrescentar os campos sem remover ou renomear os
anteriores.

A lixeira e os fechamentos passam a fazer parte do conjunto de dados do
usuário. O acompanhamento deles na nuvem depende de o serviço remoto
aceitar e salvar o JSON completo do conjunto de dados.

## 5. O que não está incluído ou não foi confirmado

É importante conhecer os limites antes de colocar a versão 2.0 em uso:

1.  **Google Apps Script:** o código do servidor não acompanha o ZIP.
    Não foi atualizado nem testado junto com esta versão.
2.  **Permissões:** os novos controles são locais e não substituem
    validações no servidor.
3.  **PIN:** não foi feita migração criptográfica do PIN. O formato
    atual foi mantido para evitar incompatibilidade com o serviço
    existente.
4.  **Sincronização Google:** não foi executado teste real de
    sincronização com a conta/planilha/serviço do usuário.
5.  **Android:** não foi executado teste de instalação real em aparelho
    Android.
6.  **Fechamento:** é fotografia de totais, não trava contábil.
7.  **Vencimentos:** são estimativas e precisam de conferência humana.
8.  **Lixeira:** só protege exclusões feitas a partir da versão 2.0.

## 6. Atualização segura do GestCard 1.3 hospedado no GitHub Pages

### Antes de começar

1.  Abra o GestCard 1.3 e gere um backup completo em JSON.
2.  Baixe o backup e guarde uma cópia fora do celular.
3.  Guarde também uma cópia dos arquivos atuais do repositório GitHub.
4.  Não desinstale o aplicativo instalado no celular.
5.  Não limpe os dados do navegador nem o armazenamento local.
6.  Não altere o `config.json` atual.

### Arquivos do pacote 2.0

No ZIP, os arquivos estão dentro da pasta `GestCard-main`.

Para a atualização descrita, substitua somente: - `index.html`; -
`sw.js`; - `version.json`.

Mantenha os arquivos atuais: - `config.json`; - `manifest.json`; -
`icon-192.png`; - `icon-512.png`; - `icon-maskable-512.png`; -
`apple-touch-icon.png`.

Não crie uma pasta `GestCard-main/GestCard-main`. Os três arquivos devem
ficar no mesmo diretório de publicação em que estavam os arquivos
antigos.

### Depois de publicar

1.  Aguarde a publicação do GitHub Pages.
2.  Abra o endereço do GestCard e confirme a versão 2.0.
3.  Entre com o perfil habitual.
4.  Confira pessoas, cartões, compras, recebimentos, acordos e saldos.
5.  Execute o diagnóstico local.
6.  Faça um novo backup JSON na versão 2.0.
7.  Teste primeiro com poucos registros e confira os resultados antes de
    usar os novos relatórios e fechamentos.

Se a versão não atualizar, não apague os dados do aparelho. Primeiro
confirme se os três arquivos foram enviados para a pasta correta e se o
GitHub Pages publicou o commit.

## 7. Recomendações para o primeiro uso

-   Confira os dias de fechamento e vencimento de cada cartão.
-   Confira os meses de referência das compras e recebimentos.
-   Não feche um mês antes de revisar os totais.
-   Trate o painel de vencimentos como uma lista de conferência, não
    como cobrança automática.
-   Teste a lixeira com um registro de baixo risco antes de depender
    dela.
-   Gere backups JSON regulares e guarde-os fora do aparelho.
-   Não use CSV, XLSX ou PDF como substituto do backup JSON.

------------------------------------------------------------------------

**Resumo:** o GestCard 2.0 acrescenta controle mensal, comparativo,
fechamento por fotografia, painel de vencimentos estimados, alertas
locais, lixeira recuperável, exportação de relatórios, permissões locais
e diagnóstico. Ele mantém os fluxos principais e a estrutura antiga do
banco, mas a atualização do servidor Google Apps Script e os testes
reais de sincronização ainda precisam ser tratados separadamente.
