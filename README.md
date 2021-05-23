# Rastreador de redes usando Wireshark e Google Maps

<hr>

Em resumo, o nosso código python vai ler um arquivo .pcap gerado pelo Wireshark, fazendo a leitura desse arquivo vamos gerar um arquivo kml e com esse arquivo em mãos vamos importar ele para o google maps mostrar a localização desejada. 



## Requisitos

### 		Documento

- [GeoLiteCity.Dat](https://github.com/mbcc2006/GeoLiteCity-data)

- Documento .pcap gerado pelo Wireshark

  Para gerar esse arquivo é preciso ter o Wireshark instalado, nele você vai fazer uma captura do tráfego da interface "Ethernet". Após a captura ser feita, você para ela(clicando no quadrado vermelho que fica na barra de navegação de cima) e no menu **File -> Export Specified Packets**, após isso salve o arquivo com o formato .pcap.

### 	Bibliotecas

- dpkt
- socket
- pygeoip

Para instalar uma biblioteca que não tenha no seu computador, é possível instalar usando o pip com o código: 

pip install <nome da biblioteca>



### Pequena explicação do código

O código depende de algumas bibliotecas externas, elas são: 

- dpkt
- socket
- pygeoip



Vamos precisar de um database que contém a geolocalização e vamos usar no código. Ele pode ser encontrado[ nesse repositório.](https://github.com/mbcc2006/GeoLiteCity-data) Junto das importações temos uma variável que vai exportar esse database.

A função main vai configurar o arquivo kml que vai ser criado para ser lido pelo Google maps. Tenha certeza de colocar o nome do arquivo .pcap capturado do Wireshark. O nome do arquivo no código está como "wire.pcap". O código de estilização do kml pode ser mudado, fiz de uma maneira simples mas que fica fácil compreender as informações que vão ser tiradas dele. É possível até trabalhar com ícones dentro do kml. 

Depois na função plotIPs temos um método que vai capturar as informações da rede e extrair os Ips do arquivo .pcap. Somente com essas informações extraídas não conseguimos fazer nada no google, pois ele não trabalha com Ips, então temos que ter uma função que vai transformar isso em Geolocalização. No código do repositório a variável "src" está preenchida com vários "x", isso porque é necessário colocar seu Ip da máquina, se você não sabe como conseguir o seu aqui está uma[ ferramenta que pode te ajudar](https://www.whatsmyip.org/). No futuro podemos automatizar a captura do Ip local para preencher ele no arquivo kml.

No final temos as linhas de código que vão executar ele. No final da execução vamos ter o arquivo kml, só vamos precisar copiar e colar o código gerado para um arquivo .kml e pronto, podemos exportar ele para dentro do[ Google Maps](https://www.google.com/maps/d/).



## Exemplo de código KML gerado pelo programa

```kml
<?xml version="1.0" encoding="UTF-8"?> 
<kml xmlns="http://www.opengis.net/kml/2.2">
<Document>
<Style id="transBluePoly"><LineStyle><width>1.5</width><color>501400E6</color></LineStyle></Style><Placemark>
<name>104.154.126.13</name>
<extrude>1</extrude>
<tessellate>1</tessellate>
<styleUrl>#transBluePoly</styleUrl>
<LineString>
<coordinates>-122.057400,37.419200
-46.641700,-23.573300</coordinates>
</LineString>
</Placemark>
<Placemark>
<name>104.154.126.13</name>
<extrude>1</extrude>
<tessellate>1</tessellate>
<styleUrl>#transBluePoly</styleUrl>
<LineString>
<coordinates>-122.057400,37.419200
-46.641700,-23.573300</coordinates>
</LineString>
</Placemark>
```









