---

copyright:
  years: 2016, 2018
lastupdated: "2018-05-08"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visão geral de recursos do {{site.data.keyword.iot_short_notm}}
{: #feature_overview}

O {{site.data.keyword.iot_full}} é construído com base nas áreas-chave a seguir:

  1. Connect - Conecte dispositivos e desenvolva aplicativos.
  2. Gerenciamento de informações - armazene, normalize, transforme e revise dados do dispositivo e integre seu {{site.data.keyword.iot_short_notm}} com outros serviços.
  3. Analytics - Especifique condições de regra que são baseadas em dados do dispositivo
em tempo real para acionar alertas e ações.
  4. Risk Management - Configure conectividade e arquitetura seguras com controle de acesso para usuários e aplicativos.

## Conectar
{: #connect}

O {{site.data.keyword.iot_short_notm}} Connect é o ponto de início para qualquer serviço do {{site.data.keyword.iot_short_notm}}. Conexão de dispositivos, criação de aplicativos, controle de seus dispositivos e interatividade com serviços de terceiros estão disponíveis no {{site.data.keyword.iot_short_notm}} Connect.

### Dispositivos de gateway

Usando um gateway, é possível conectar dispositivos ao {{site.data.keyword.iot_short_notm}} que, caso contrário, não podem se conectar à Internet. Gateways têm todas as funções de um dispositivo, mas também podem publicar e assinar em nome dos dispositivos conectados a eles. Os dispositivos de gateway permitem que grupos de sensores que não podem se conectar à Internet conectem-se ao seu {{site.data.keyword.iot_short_notm}} enviando seus dados a um gateway. Para obter mais informações, consulte [desenvolvendo para gateways](https://console.ng.bluemix.net/docs/services/IoT/gateways/gw_dev_index.html).

### Gerenciamento de dispositivo

Os recursos de gerenciamento de dispositivo são fornecidos por meio de uma API de gerenciamento de dispositivo e um agente de gerenciamento de dispositivo instalado nos dispositivos. Os dispositivos com um agente de gerenciamento de dispositivo podem executar ações de gerenciamento de dispositivo, que podem ser acionadas por meio do painel principal do {{site.data.keyword.iot_short_notm}} ou da API de gerenciamento de dispositivo. As ações de gerenciamento de dispositivo incluem reinicializar, fazer download e instalar atualizações de firmware, e reconfigurar dispositivos para configurações de fábrica. O gerenciamento de dispositivo pode também ser estendido para incluir ações customizadas de gerenciamento de dispositivo. Para obter mais informações, consulte a [documentação de gerenciamento de dispositivo](https://console.ng.bluemix.net/docs/services/IoT/devices/device_mgmt/index.html).

### Extensões e integrações de serviço

Extensões e integrações de serviço permitem que serviços externos e extensões definidas pelo usuário de serviços principais sejam incluídos em uma instância do {{site.data.keyword.iot_short_notm}}. Os serviços externos que podem ser integrados
com o {{site.data.keyword.iot_short_notm}} incluem os serviços de localização de clima
The Weather Company, permitindo que você saiba o clima atual em uma localização de dispositivo
e dados SIM Jasper. Para obter mais informações sobre extensões e integrações de serviços de terceiros, consulte [integrando serviços externos](https://console.ng.bluemix.net/docs/services/IoT/reference/extensions/index.html).

---

## Gerenciamento das informações
{: #information_management}

O {{site.data.keyword.iot_short_notm}} Information Management controla os dados que são enviados por dispositivos após atingirem seu serviço do {{site.data.keyword.iot_short_notm}}. Information Management inclui armazenamento de dados e transformação.

### Cache do último evento do dispositivo

Usando a API (interface de programação de aplicativos) de cache do último evento do {{site.data.keyword.iot_short_notm}}, é possível recuperar o último evento que foi enviado por um dispositivo. Isso funciona estando o dispositivo on-line ou off-line, o que permite recuperar o status do dispositivo independentemente da localização física do dispositivo ou do status de uso. Os últimos dados do evento de um dispositivo podem ser recuperados para qualquer evento específico que tenha ocorrido até 45 dias atrás.

### Armazenamento de dados do evento de dispositivo

Os dados de evento de dispositivo de seu serviço do {{site.data.keyword.iot_short_notm}} podem ser armazenados para uso posterior. O armazenamento de dados é uma primeira etapa essencial para realizar análises de dados criteriosas para obter insights a partir desses dados.  Por exemplo, é possível rastrear mudanças por períodos de tempo mais longos e armazenar conjuntos de dados para uso com ferramentas de análise de dados poderosas, incluindo uso com APIs (interfaces de programação de aplicativos) do Watson e computação cognitiva. Para obter mais informações, consulte [conectando um {{site.data.keyword.cloudant_short_notm}} serviço historiador](https://console.ng.bluemix.net/docs/services/IoT/cloudant_connector.html) ou [conectando um {{site.data.keyword.messagehub}} serviço historiador](https://console.ng.bluemix.net/docs/services/IoT/message_hub.html).

### Gerenciamento de dados

Diferentes marcas e modelos de dispositivos publicam dados em formatos diferentes. O
recurso de gerenciamento de dados permite transformar e normalizar esses dados em uma
única visualização lógica chamada *estado do dispositivo*, que pode ser
entendida e processada por aplicativos. O uso do recurso de gerenciamento de dados
simplifica muito o desenvolvimento de aplicativos porque o aplicativo não precisa mais
entender os diferentes formatos dos dados do evento que são enviados de cada dispositivo. Quando
os dispositivos publicam eventos no {{site.data.keyword.iot_short_notm}}, o
conteúdo dos eventos pode ser mapeado para as propriedades do estado definido pelo
usuário usando mapeamentos. Se o evento de entrada resultar em uma mudança no estado do
dispositivo, os valores das propriedades de estado do dispositivo serão atualizados e
armazenados no {{site.data.keyword.iot_short_notm}}. Os valores são
disponibilizados ao aplicativo na solicitação usando uma API HTTP ou assinando um
tópico.

Para obter mais informações sobre como usar esse recurso, consulte
[Introdução ao gerenciamento
de dados](GA_information_management/ga_im_device_twin.html).

---

## Analytics
{: #analytics}

### Edge e análise de nuvem

Usando análise de dados de nuvem do {{site.data.keyword.iot_short_notm}}, você especifica as condições das regras que são baseadas em dados do dispositivo de tempo real e que acionam alertas e ações opcionais quando atendidas. Por exemplo, você pode criar uma regra para assegurar que quando o dispositivo for descartado ou quando a temperatura do dispositivo aumentar, um alerta será enviado ao painel do dispositivo de um usuário e um e-mail será enviado ao administrador. Para obter mais informações, consulte a [documentação da análise de nuvem](https://console.ng.bluemix.net/docs/services/IoT/cloud_analytics.html).

Com Edge Analytics, você move o processo de acionamento da regra de análise de dados da nuvem para um gateway ativado por Edge Analytics que pode reduzir de forma drástica a quantia de tráfego de dados do dispositivo para a nuvem executando o processamento de análise de dados próximo ao dispositivo. Para obter mais informações, consulte a [documentação do Edge Analytics](https://console.ng.bluemix.net/docs/services/IoT/edge_analytics.html).

---

## Gerenciamento de Risco
{: #risk_management}

### Conectividade e arquitetura seguras

A arquitetura do {{site.data.keyword.iot_short_notm}} é projetada para evitar que dispositivos personifiquem outros dispositivos, o que mantém a integridade de seus dados do dispositivo. Os dispositivos se conectam ao {{site.data.keyword.iot_short_notm}} usando uma combinação de um identificador de cliente e um token de autenticação que somente você conhece. Após os dispositivos serem registrados ou as chaves API (interface de programação de aplicativos) serem geradas, é efetuado salt e hash do token de autenticação para manter a segurança de suas credenciais.

O complemento Gerenciamento de Risco e Segurança permite aprimorar a segurança do {{site.data.keyword.iot_short_notm}} para assegurar que todos os pontos de conexão entre o servidor e os dispositivos sejam autenticados com credenciais comprovadas. Com este complemento, os certificados e a autenticação Transport Layer Security (TLS) são usados, na parte superior do uso de {{site.data.keyword.iot_short_notm}} de IDs de usuário e tokens. Durante a comunicação entre dispositivos e o servidor, quaisquer dispositivos que não tenham certificados válidos com acesso ao servidor, como configurado no complemento Gerenciamento de Risco e Segurança, têm o acesso negado, mesmo que usem IDs de usuário e senhas válidos.

---
