# Gerene.DFe.EscPos

[![Nuget count](http://img.shields.io/nuget/v/Gerene.DFe.EscPos.svg)](https://www.nuget.org/packages/Gerene.DFe.EscPos)

Impressão em impressora termica para DFes via EscPos e derivados (EscBema, EscDaruma, EscElgin, entre outros) nativo em .NET.

Atualmente a biblioteca atende os documentos SAT e NFCe nos formatos 58 e 80mm.

Permite comunicação via RAW (USB), TCP e Serial.


Funcionamento:
----

O projeto é construído em .Net Standard 2.0 e conta com dois demos (.Net Framework 4.6.2 e .Net 6).

Exemplo de uso:
```
using (var _printer = new SatPrinter()) //ou new NFCePrinter() para NFCe
{
	_printer.Protocolo = ProtocoloEscPos.EscPos; //Protocolo de comunicação	
	_printer.Impressora = "Nome da impressora"; //Para RAW nome da impressora. Para TCP o IP da impressora na rede. Para serial a porta.
	_printer.CortarPapel = true;
	_printer.ProdutoDuasLinhas = false;
	_printer.UsarBarrasComoCodigo = false;
	_printer.DocumentoCancelado = false; //Exibe tarja "Documento cancelado na impressão"
	_printer.Logotipo = logotipo_em_bytes; //Impressão do logotipo, não obrigatório
	_printer.TipoPapel = TipoPapel.Tp80mm; //ou TipoPapel.Tp58mm
	
	_printer.TipoConexao = TipoConexao.RAW; //padrão RAW, não obrigatório para conexão USB
	_printer.RemoverAcentos = true; //padrão true, não obrigatório
	
	_printer.Imprimir(string_com_o_conteudo_do_xml); //Imprime o documento fiscal
	
	// para impressão específica do XML de cancelamento de SAT CF-e use:
        //_printer.ImprimirCancelamento(string_com_o_conteudo_do_xml_de_cancelamento);
}
```


Dependências:
----

OpenAC.Net.EscPos (motor de impressão) - https://github.com/OpenAC-Net/OpenAC.Net.EscPos

OpenAC.Net.Sat (desserialização do xml do SAT) - https://github.com/OpenAC-Net/OpenAC.Net.Sat

DFe.Net (desserialização do xml da NFCe) - https://github.com/ZeusAutomacao/DFe.NET


Change log:
----
1.0.18 - Atualizando referencias ao Zeus (remoção dos projetos shared)

1.0.17 - Altera o motor de impressão, adicionando os protcolos TCP e Serial e novos recursos como impressão de caracteres acentuados.

1.0.16 - Remove o @ que aparecia no meio do protocolo no NFCe

1.0.15 - Migrando para OpenAC.Net.Sat

1.0.14 - Opção de alterar casas decimais da quantidade

1.0.13 - Melhora na impressão da observação do contribuinte

1.0.12 - SAT quebrava se o XFant de emitente estivesse nulo

1.0.11 - Opção de ocultar tag "De olho no imposto"

1.0.10 - Não era possível imprimir NFCe sem a tag infAdic (issue #6)

1.0.9 - Impressão em 58mm

1.0.8 - Adiciona a impressão do logotipo

1.0.7 - Adiciona Qtde. total de itens"

1.0.6 - Impressão para cancelamento do SAT



Break changes:
----

A versão 1.0.17 traz um novo motor de impressão (OpenAC.Net.EscPos) que permite impressão RAW (padrão para comunicação USB identica ao comportamento anterior) e adiciona os protocolos TCP e Serial.

Você pode preencher apenas o atributo "Impressora" (antes chamado de "NomeImpressora") e substituir o atributo "TipoImpressora" por "Protocolo" e o comportamento do motor anterior será mantido.



Outras configurações:
----

Com o novo motor, além dos novos protocolos, existe um controle mais apurado da impressora.

Os atributos "ConfiguracaoRAW", "ConfiguracaoTCP" e "ConfiguracaoSerial" permitem alterações no comportamento da impressora e na forma de comunicação, para mais informações confira o funcionamento em https://github.com/OpenAC-Net/OpenAC.Net.EscPos


Licença:
---- 

A licença do projeto é MIT, o seu uso é livre. Não garantimos QUALQUER suporte.



Agradecimentos:
----

O projeto Vip.Printer (https://github.com/leandrovip/Vip.Printer) serviu de motor de impressão entre as versões 1.0.0 e 1.0.16 de forma gratuíta e com qualidade, permitindo o funcionamento dessa biblioteca por quase dois anos com um nível muito baixo de manutenção.

Em busca de evolução a troca de motor foi necessária na versão 1.0.17. Essa mudança permitiu novos protocolos e o uma parceria ainda mais estreita com o grupo OpenAC que vem fazendo um trabalho incrível com diversos componentes para automação comercial. Conheça mais em: https://github.com/OpenAC-Net
