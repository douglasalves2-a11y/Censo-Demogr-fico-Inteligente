IBGE Nomes – Nomes mais comuns por localidade (Censo 2022)

Aplicativo .NET MAUI que consome, de forma encadeada, duas APIs públicas do IBGE para mostrar os nomes mais comuns de homens e mulheres, além dos sobrenomes, de um estado ou município brasileiro.

Atividade da disciplina de Tecnologias Móveis – UNIS (Centro Universitário do Sul de Minas) – Análise e Desenvolvimento de Sistemas.

👥 Integrantes
Douglas Henrique Alves
🎯 Objetivo

Permitir que o usuário selecione uma localidade e visualize instantaneamente os nomes mais frequentes daquela região, usando consumo dinâmico de APIs abertas (sem bases estáticas).

🔗 Fluxo de funcionamento (consulta encadeada)
Ao iniciar, o app consulta a API de Localidades e popula o Picker de Estados.
Ao escolher um estado, o app carrega os Municípios daquele estado no segundo Picker e já consulta os nomes do estado.
Ao escolher um município, o app consulta os nomes do município.
Cada consulta usa o id da localidade na API de Nomes (Censo 2022).
O JSON é processado e exibido em três listas: Homens, Mulheres e Sobrenomes.
🌐 APIs utilizadas
API	Endpoint
Localidades – Estados	https://servicodados.ibge.gov.br/api/v1/localidades/estados
Localidades – Municípios por estado	https://servicodados.ibge.gov.br/api/v1/localidades/estados/{id}/municipios
Nomes por localidade (Censo 2022)	https://servicodados.ibge.gov.br/api/v3/nomes/2022/localidade/{id_localidade}

Documentação oficial: https://servicodados.ibge.gov.br/api/docs

🏗️ Arquitetura em camadas
IbgeNomes/
├── Models/
│   ├── Localidade.cs        # Estado e Municipio (mapeiam o JSON de localidades)
│   └── NomeFrequencia.cs    # NomeFrequencia e NomesLocalidade (resultado da API de nomes)
├── Services/
│   └── IbgeService.cs       # HttpClient, requisições e desserialização JSON
├── Views/
│   ├── MainPage.xaml        # Pickers e CollectionViews
│   └── MainPage.xaml.cs     # Eventos de UI e chamada ao serviço
├── App.xaml / MauiProgram.cs
└── README.md
Camada	Responsabilidade
Apresentação (Views)	Elementos visuais: Picker, CollectionView, indicador de carregamento
Serviços (Services)	Comunicação HTTP com as APIs do IBGE e tratamento do JSON
Modelos (Models)	Classes que representam os dados recebidos (Estado, Município, Nome, Frequência)
⚙️ Pré-requisitos
.NET SDK 8.0 ou superior
Workload do MAUI instalada:
bash
dotnet workload install maui
Visual Studio 2022 (17.8+) com a carga de trabalho Desenvolvimento de aplicativos móveis com .NET, ou VS Code com a extensão .NET MAUI
Emulador Android configurado (Android SDK) ou dispositivo físico com depuração USB
Conexão com a internet (as APIs são consumidas em tempo real)
▶️ Como executar
Clone o repositório:
bash
git clone <URL_DO_REPOSITORIO>
cd IbgeNomes
Restaure as dependências:
bash
dotnet restore
Inicie um emulador Android (ou conecte um dispositivo).
Execute o app:
bash
dotnet build -t:Run -f net8.0-android

No Visual Studio: selecione o emulador Android como destino e pressione F5.

A permissão INTERNET já deve estar presente no AndroidManifest.xml.

📱 Como usar
Aguarde o carregamento da lista de estados.
Selecione um estado – as listas de nomes aparecem automaticamente.
(Opcional) Selecione um município para ver os nomes específicos dele.
⚠️ Observações
O IBGE não divulga resultados quando a quantidade de ocorrências é pequena demais, então algumas localidades podem retornar poucos dados ou nenhum.
O app exibe mensagem de erro caso a API esteja indisponível ou sem conexão.
🎥 Vídeo de demonstração

Link do vídeo (YouTube ou Google Drive)

🛠️ Tecnologias
.NET MAUI
C#
HttpClient e System.Text.Json
APIs abertas do IBGE
