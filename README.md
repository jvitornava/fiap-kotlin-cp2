# fiap-kotlin-cp2
João Vitor Nava  - RM: 98623

Obs:  Professor, não consegui rodar o projeto na minha maquina, porem a partir do seu repositorio, elaborei o READ.ME

Execução Inicial da MainActivity
No momento em que a MainActivity é criada, o método onCreate(Bundle?) é automaticamente acionado como parte do ciclo de vida padrão de uma activity no Android. Esse método executa diversas configurações essenciais e invoca outras funções, algumas até mais de uma vez.

super.onCreate(savedInstanceState): Responsável por garantir que a activity seja corretamente inicializada, restaurando seu estado anterior e preparando todos os recursos do sistema Android.

findViewById(...): Recupera elementos visuais definidos no layout XML da aplicação, por meio do identificador associado no recurso res.

configureToolBarMain(toolbar): Configura a barra de ferramentas da interface. Define atributos como o texto do título, cores visuais e aparência de fundo, com os valores obtidos de arquivos como strings.xml e colors.xml. Também integra a toolbar à SupportActionBar.

btnRefreshButton.setOnClickListener { makeCallRequest() }: Define o comportamento do botão de atualização. Quando pressionado, ele aciona a função makeCallRequest, responsável por obter dados atualizados do valor do Bitcoin.

Comunicação com a API: makeCallRequest()
Essa função inicia uma instância do serviço MercadoBitcoinService usando uma fábrica (MercadoBitcoinServiceFactory), que aplica o padrão de projeto Factory para criar dinamicamente objetos.

Com a instância criada via create(), é feita uma chamada HTTP por meio da função getTicker(), que acessa o endpoint da API e retorna os dados encapsulados em uma Response<TickerResponse>.

Após receber a resposta, o método avalia se a requisição foi bem-sucedida (códigos de status 2XX). Em caso positivo, extrai o campo lastValue do corpo da resposta e o exibe no campo lblValue.text, caso o valor não seja nulo.

A data e hora da consulta são formatadas com um objeto SimpleDateFormat e exibidas no campo lblDate.text.

Caso ocorram falhas, como erros HTTP 400, 401, 403, 404 ou falhas desconhecidas, esses cenários são tratados adequadamente.

Detalhes Técnicos do Serviço
A interface MercadoBitcoinService define o acesso ao endpoint api/BTC/ticker/ usando Retrofit, com a anotação @GET e a palavra-chave suspend, que indica operação assíncrona – evitando bloqueio da thread principal.

Criação do Serviço: MercadoBitcoinServiceFactory
A fábrica de serviços MercadoBitcoinServiceFactory segue o padrão Factory para configurar uma instância de Retrofit com:

A URL base da API

O conversor Gson, que transforma automaticamente os dados JSON recebidos em objetos Kotlin.

O método create() devolve uma implementação da interface MercadoBitcoinService, pronta para uso em chamadas HTTP.

