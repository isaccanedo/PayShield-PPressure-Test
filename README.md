# PayShieldPPressureTest
:computer: # Ferramenta para gerar carga de trabalho no PayShield 10k ou 9k para fins de teste e demonstração

O script Python pressureTest.py cria uma carga de trabalho nos dispositivos Thales payShield 10k e 9k. O script pode ser útil durante as demonstrações dos recursos de monitoramento do dispositivo e pode ser usado em todos os casos em que você precisar gerar uma carga de trabalho para fins de teste.

Requer Python 3. Ele foi testado em Python 3.7 e 3.8 usando um payShield 10k.

# 1. Uso
```
pressureTest.py [-h] [--port PORT] [--proto {tcp, udp, tls}] [--keyfile CLIENT.KEY] [--crtfile CLIENT.CRT] 
[--key {2048,4096} | --nc | --j2 | --j4 | --n8 | --jk | --randgen] [--head HEADER] [--forever] 
[--times TIMES] host
```

host, você precisa especificar o endereço IP ou o nome do host / fqdn do dispositivo payShield.
```
--port especifica a porta do host. Se o parâmetro for omitido, o valor padrão 1500 é usado.
```

```
--proto especifica o protocolo a ser usado, tcp, udp ou tls. Se o parâmetro for omitido, 
o valor padrão tcp será usado. Se tls for usado, você pode especificar o caminho do arquivo 
de chave do cliente e do certificado usando os parâmetros --keyfile e --crtfile
```

```
--keyfile o caminho do arquivo de chave do cliente. Se não for especificado, 
o valor padrão é client.key. É apenas considerado se o protocolo é tls
```
```
--crtfile o caminho do arquivo de certificado do cliente. Se não for especificado, 
o valor padrão é client.crt. É apenas considerado se o protocolo é tls
```

```
--key o comprimento da chave RSA que o dispositivo irá gerar. existem apenas dois valores válidos: 
2048 ou 4096. se o parâmetro não for especificado, 2048 é o padrão.
```

```
--header a string do cabeçalho para prefixar o comando do host. se não for especificado, 
o valor padrão é HEAD.
```

```
--nc executa apenas um teste NC. Não pode ser usado em conjunto com --key.
```

```
--j2 obtém o carregamento do HSM usando o comando J2. Não pode ser usado em conjunto com --key.
```

```
--j4 obtém Volumes de Comando do Host usando o comando J4. Não pode ser usado em conjunto com --key.
```

```
--j8 obtém as contagens acumuladas de verificação de integridade usando o comando J8. Não pode ser usado em conjunto com --key.
```

```
--jk obtém o status da verificação de saúde instantânea usando o comando JK. Não pode ser usado em conjunto com --key.
```

```
--randgen Gera um valor aleatório de 8 bytes usando o comando N0. Não pode ser usado em conjunto com --key.
```

```
--para sempre o teste será executado para sempre. Use CTRL-C para encerrá-lo.
```

```
--vezes quantas vezes executa o teste. Se não for especificado, o valor padrão é 1000 vezes.
```

# 2. Exemplo

```
C:\Test>python pressureTest.py 192.168.0.36 --nc --times 2
```

Utilitário de estresse do PayShield, para obter mais informações sobre o uso, invoque-o com a 
opção -h Este software é de código aberto e está sob o Affero AGPL 3.0

### 2.1. Iteração: 1 de 2

```
Código de retorno: 00 Sem erro Comando enviado/recebido: NC ==> Dados enviados ND (ASCII): 
b'HEADNC 'dados enviados (HEX): b'0006484541444e43' dados recebidos (ASCII): 
b'HEADND005D672700000000001500-0023 'dados recebidos (HEX): b'0021484541444e44303035443637323730303030303030303030313530302d30303233 '
```

### 2.2. Iteração: 1 de 2

```
Código de retorno: 00 Sem erro Comando enviado / recebido: NC ==> Dados enviados ND (ASCII): 
b'HEADNC 'dados enviados (HEX): b'0006484541444e43' dados recebidos (ASCII): 
b'HEADND005D672700000000001500-0023 'dados recebidos (HEX): b'0021484541444e44303035443637323730303030303030303030313530302d30303233 '
```

# 4. NOTAS
O comando EI usado para gerar a chave RSA requer autorização e a geração de chaves de 4.096 bits só é possível para keyblock LMKs.
