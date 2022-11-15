# Exemplo prático de um Block Magento 1
Como é a estrutura básica para um módulo com um bloco de template funcionar no Magento 1.

<h2>Mas o que são os blocks?</h2>
Tudo no frontend do Magento é exibido atavés de blocos, e neles determinamos as linhas.

<h2>Ondem ficam os blocks?</h2>
Possuem uma pasta dedicada dentro da raiz do seu módulo, a pasta <strong>Block</strong> e os arquivos podem ter qualquer nome.php

---
Será necessário apenas alguns arquivos para fazer o bloco funcionar, sendo eles:

<strong>app/code/local/Elnogara/Firstblock/etc/config.xml

app/code/local/Elnogara/Firstblock/Block/Hello.php

app/design/frontend/base/default/layout/elnogara_firstblock.xml

app/design/frontend/base/default/template/firstblock/world.phtml

app/etc/modules/Elnogara_Firstblock.xml</strong>


Vamos começar pelo config.xml que é o arquivo responsável por declarar todo o funcionamento do módulo:
```
<?xml version="1.0" encoding="UTF-8"?>
<config>
    <modules>
        <Elnogara_Firstblock>
            <version>1.0.0</version>
        </Elnogara_Firstblock>
    </modules>
	<global>
		<blocks> <!--Aqui você declara que vai utilizar blocos-->
      		<elnogara_firstblock> <!--É necessário dar um apelido para a pasta dos seus blocks assim como é feito para os helpers-->
				<class>Elnogara_Firstblock_Block</class> <!--E então é necessário apontar qual o caminho da sua pasta que contém os blocks-->
	 		</elnogara_firstblock>
	    </blocks>
	</global>
    <frontend> <!--Dentro da tag frontend pois eles serão utilizados no front da loja-->
        <layout> <!--Será apontado um arquivo de layout-->
            <updates>
                <elnogara_firstblock> <!--Aqui você está declarando um nome para o seu arquivo de layout-->
                    <file>elnogara_firstblock.xml</file> <!--E nesse nó você está passando qual arquivo de layout está sendo referênciado-->
                </elnogara_firstblock>
            </updates>
        </layout>
    </frontend>
</config>
```

Em sequência do config.xml será chamado o arquivo de layout para avaliar as configurações dentro dele, segue abaixo o código:
```
<?xml version="1.0"?>
<layout> <!--Será uma alteração de layout-->
    <default> <!--Muito importante entender que são os handles do Magento, e ele filtra em quais páginas o seu layout será executado, com o handle default significa que esse layout vai ser executado em todas as páginas da loja.-->
        <reference name="top.container">  <!--Também é necessário referênciar um bloco que já existe no Magento, sendo assim o seu vai ser printado apartir desse-->
            <block name="helloworldy" type="elnogara_firstblock/hello" template="firstblock/world.phtml"></block> <!--Muita atenção nessa parte, esse nó block recebe 3 parâmetros importantes, name=Nome do seu bloco ELE DEVE SER ÚNICO se não não funciona, type=Será sempre passado o bloco que será criado dentro da raiz do módulo na pasta Block, template=É o arquivo de template que vai ser carregado no frontend é nele que fica a parte visível para o usuário-->
        </reference>
    </default>
</layout>
```

Após isso, bem simples é necessário criar o arquivo de template, segue abaixo o código dele:
```
<h1>Hello World! NOGARA</h1> <!--Será apenas para exemplo, mas é aqui onde escolhemos o que será carregado pelo seu bloco no frontend-->
```

Pra finalizar, criar o arquivo Hello.php que deve existir para que o template sejá printado corretamente na tela, com o código abaixo:
```
<?php
class Elnogara_Firstblock_Block_Hello extends Mage_Core_Block_Template{

}
```

Não se esqueça de criar o arquivo de ativação do módulo dentro de etc/modules:
```
<?xml version="1.0" encoding="UTF-8"?>
<config>
	<modules>
		<Elnogara_Firstblock>
			<active>true</active>
			<codePool>local</codePool>
		</Elnogara_Firstblock>
	</modules>
</config>
```

Agora basta acessar a home da sua loja e ver que você printou um bloco no 'top.container', que ficará próximo ao menu de navegação da sua loja.

<strong>Qualquer dúvida estou a disposição - <a href="https://wellingtonnogara.com/" style="color: red;">Wellington Nogara</a>.</strong>
