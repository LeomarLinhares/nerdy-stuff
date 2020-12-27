# Vantagens e desenvolvimento de Web Services :spider_web:

### O que são Web Services? :thinking:

Web Services são soluções para que aplicações se comuniquem independente de linguagem, softwares e hardwares utilizados.

Existe portanto uma troca de mensagens entre aplicações diferentes por meio de uma linguagem de marcação como XML ou JSON.

###### Vantagens:

- Linguagem comum
- Integração facilitada
- Reutilização de implementação
- Segurança
- Custos

###### Principais Tecnologias

- SOAP (arquitetura)
- REST (arquitetura)
- XML (linguagem de marcação)
- JSON (linguagem de marcação)

***

### Estrutura SOAP 🧼

1. O que é SOAP?

SOAP - Simple Object Access Protocol

É um protocolo baseado em XML para acessar Web Services principalmente por HTTP. Em outras palavras, uma definição (arquitetura) de como serviços web se comunicam.

Meio de transporte genérico, pode ser usado por outros protocolos além do HTTP.

2. O que é XML?

XML - Extensible Markup Language

É uma linguagem de marcação criada na década de 90 pela W3C que facilita a separação de conteúdos sem limitação de tags (etiquetas).

3. Estrutura SOAP

```xml
<soap:Envelope>
    <!-- 
	Envelope encapsula toda a mensagem e contém dentro de si o Header e o Body 
	-->
	<soap:Header>
        <!-- 
        Header possuí informações de atributos e metadados da requisição.
		Exemplos: IP de origem, token, DNS, credenciais de autenticação, etc.
         -->
    </soap:Header>
    
    <soap:Body>
        <!-- 
		Body contém os detalhes da mensagem 
		Onde ficam os dados.
		-->
    </soap:Body>
</soap:Envelope>
```

Exemplo prático:

```xml
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
    <soap:Header>
    </soap:Header>
    <soap:Body>
        <m:MetodoEndereco xmlns:m="http://www.example.org/endereco">
            <m:Cidade>Rio de Janeiro</m:Cidade>
            <m:CEP>00000-00</m:CEP>
            <m:Logradouro>Avenida Exemplar do Exemplo</m:Logradouro>
            <m:Numero>00</m:Numero>
        </m:MetodoEndereco>
    </soap:Body>
</soap:Envelope>
```

---

### Entendendo o que é WSDL e XSD :sun_with_face:

1. O que é WSDL?

WSDL - Web Services Description Language

Usado para descrever Web Services, como um contrato de serviço. A descrição é feita em um documento XML, onde é descrito o serviço, especificações de acesso, operações e métodos.

Basicamente dita as informações que vão estar contidas na SOAP Message por meio de uma estrutura.

2. O que é XSD?

XSD - XML Schema Definition

É um schema no formato XML usado para definir a estrutura de dados que será validada no XML. Como uma documentação de como deve ser montado o SOAP Message que será enviado através do Web Service.

---

### Aprenda o que são REST, API e JSON :gear:

1. O que é REST?

REST - Representational State Transfer

Faz uma chamada da representação de como o objeto está naquele determinado momento. Diferente do SOAP o REST não é um protocolo, é um estilo de arquitetura.

Ele pode trabalhar com outros formatos como XML, JSON ou outros. Sua arquitetura é de fácil compreensão.

2. Dinâmica estrutural

O **CLIENTE** faz uma requisição HTTP ao **SERVIDOR** utilizando algum método de requisição (GET, POST, PUT, DELETE...) e o **SERVIDOR** retorna um código de operação (que informam coisas como se a operação teve sucesso ou não) e a mensagem (Texto, JSON, XML...).

Quando uma aplicação web disponibiliza um conjunto de rotinas ou padrões através de serviços web, podemos chamar esse conjunto de API.

3. O que é API?

API - Application Programming Interface

São conjuntos de rotinas documentados e disponibilizados por uma aplicação para que outras aplicações possam consumir suas funcionalidades.

4. Principais métodos HTTP

- GET: Solicita a representação de um recurso
  - O objeto como estava no momento em que foi requisitado
- POST: Solicita a criação de um recurso
- DELETE: Solicita a exclusão de um recurso
- PUT: Solicita a atualização de um recurso

Há mais métodos, mas esses são os principais.

5. O que é JSON?

JSON - JavaScript Object Notation

Formatação leve utilizada para troca de mensagem entre sistemas que utiliza de uma estrutura de **chave** e de **valor** e também de **listas ordenadas**.

Exemplo de estrutura JSON:

```json
{
    "nome": "Os Vingadores",
    "ano_lancamento": "2019",
    "personagens": [
        {
            "nome": "Thanos"
        },
        {
            "nome": "Homem de Ferro"
        },
        {
            "nome": "Thor"
        }
    ]
}
```

---

### Integração com REST e métodos HTTP na prática :computer:

1. **Códigos de Estado:** representam o estado de uma operação solicitada.
   - **1xx** - Informativo
   - **2xx **- Sucesso
   - **3xx** - Redirecionamento
   - **4xx** - Erro do Cliente
   - **5xx** - Erro do Servidor

Detalhamento dos códigos disponível em [Mozilla: Códigos de status de respostas HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status).