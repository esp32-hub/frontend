# Frontend — ESP32 Sensor Monitor

Dashboard web para visualização das leituras de sensores enviadas por dispositivos ESP32, consumindo a API do [Backend-PHP](../Backend-PHP/).

> 🚧 **Status v1:** Em desenvolvimento

## Stack

- **Interface:** HTML5, Tailwind CSS (via CDN)
- **Lógica:** JavaScript (Vanilla)
- **Comunicação:** Fetch API (HTTP GET → `listar.php`)

## Estrutura do Repositório

```
frontend/
└── index.html      # Aplicação completa (single-file)
```

## Configuração

A URL da API é definida diretamente no `index.html`:

```js
const API_BASE = 'http://localhost/Backend-PHP/listar.php'
```

Altere o valor de `API_BASE` para apontar ao endereço correto do backend antes de abrir no navegador.

## Como Usar

Não requer instalação ou build. Basta abrir o `index.html` diretamente no navegador ou servir via qualquer servidor HTTP estático.

---

## Interface

### Cards de Resumo

Exibidos no topo da página, atualizam a cada ciclo de busca:

| Card               | Descrição                                  |
|--------------------|--------------------------------------------|
| Total de Leituras  | Quantidade total de registros no banco     |
| Última Temperatura | Valor de temperatura da leitura mais recente |
| Última Umidade     | Valor de umidade da leitura mais recente   |

### Tabela de Leituras

Exibe os registros paginados retornados pela API:

| Coluna      | Descrição                                         |
|-------------|---------------------------------------------------|
| #           | ID do registro                                    |
| Temperatura | Valor em °C                                       |
| Umidade     | Valor em %                                        |
| Predição    | Badge colorido conforme o valor retornado         |
| Data / Hora | Timestamp convertido para `America/Sao_Paulo`     |

#### Badges de Predição

| Valor     | Cor         |
|-----------|-------------|
| `normal`  | Verde       |
| `alerta`  | Amarelo     |
| `critico` | Vermelho    |
| outros    | Cinza neutro |

### Paginação

Controlada pelos parâmetros `limit` e `offset` da API:

- Seletor de registros por página: `10`, `25`, `50` (padrão), `100`
- Botões **Anterior** / **Próxima** com estado desabilitado nos limites
- Contador de posição: `X–Y de Z`

---

## Comportamentos

- **Auto-refresh:** os dados são recarregados automaticamente a cada **30 segundos**
- **Timestamp:** exibido no cabeçalho indicando o horário da última atualização
- **Estado de carregamento:** mensagem exibida enquanto a requisição está em andamento
- **Tratamento de erro:** mensagem descritiva exibida em caso de falha na requisição

---

## Paleta de Cores

| Papel         | Cor                        |
|---------------|----------------------------|
| Fundo         | Preto (`#000000`)          |
| Texto         | Branco (`#ffffff`)         |
| Destaque      | Verde-esmeralda (`#10b981`) |

---

## Requisitos Funcionais (RF)

- [x] Exibir o total de leituras registradas no banco;
- [x] Exibir a temperatura e umidade da leitura mais recente;
- [x] Listar todas as leituras em formato tabular;
- [x] Permitir paginação via seletor de registros por página;
- [x] Diferenciar visualmente os valores de predição por cor.

## Requisitos Não-Funcionais (RNF)

- [x] Não requer build, bundler ou dependências instaladas localmente;
- [x] Tailwind CSS carregado via CDN;
- [x] Interface responsiva para diferentes tamanhos de tela;
- [x] Atualização automática periódica sem interação do usuário.

## Regras de Negócio (RN)

- [x] A paginação deve resetar para a primeira página ao alterar o limite por página;
- [x] Datas devem ser exibidas no fuso horário `America/Sao_Paulo`;
- [x] Erros retornados pela API devem ser exibidos na interface sem quebrar a aplicação.
