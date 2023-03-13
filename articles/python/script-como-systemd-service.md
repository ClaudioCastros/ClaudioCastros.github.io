# Python Script como um Serviço do Systemctl/Systemd

Há várias formas de manter seus programas em execução no backgroud do Linux como por exemplo usando o **crontab**, **.bashrc**, etc e outra forma é utilizando o **systemd**.

A maioria das versões de linux já tem o pacote do systemd pré instalado, mas caso ainda não o tenha é possivel sim realizar
a instalação como qualquer outro pacote comum. 

Nota: Nos testes deste artigo estarei utilizando **Ubuntu 20.04 LTS**

Para verificar se o systemd já está instalado utilize o seguinte comando:

```bash
systemd --version
```
Caso o seu SO não tenha o systemd instalado utilize o comando abaixo para instalar

```bash
sudo apt-get install systemd -y
```
## Exemplo de Script Python

Como o objetivo é explicar como executar um script usando o systemd vamos criar um script simples para isso, irei dar o nome de **systemd-teste.py**

```python
import time
from datetime import datetime

while True:
    with open("output.txt", "a") as f:
        f.write(f"O timestamp atual é: {str(datetime.now())}")
        f.close()
        time.sleep(5)
```

O script acima irá escrever o timestamp atual no arquivo output.txt a cada 5 segundos.

O próximo passo é escrever o serviço no systemd.

## Arquivo de Serviço - unit

O arquivo de serviço deve ser criado dentro do diretório **/etc/systemd/system/teste.service** (Neste caso o nome do serviço será **teste**).

```
[Unit]
Description=Meu Serviço de Teste
After=multi-user.target

[Service]
Type=simple
Restart=always
ExecStart=/usr/bin/python3 /home/<username>/systemd-python.py

[Install]
WantedBy=multi-user.target
```

Altere o valor de <username> pelo nome do seu usuário no linux. A flag **ExecStart** contém o comando que será executado
, então basicamnete o primeiro argumento é caminho de onde está o o binário do python que será responsável pela execução do script,
o segundo argumento é o caminho do script que será executado.
A flag **Restart** indica que o script passará por um restart em caso de o sistema operacional reiniciar.
  
Por ultimo é necessário realizar um reload no daemon para que o novo serviço seja detectado pelo systemd.
  
```bash
sudo systemctl daemon-reload
```
  
Para que o novo serviço criado seja iniciado sempre que o SO iniciar é necessário ativar ele como **enable**.
 
```bash
sudo systemctl enable systemd-python.service
```
Agora vamos iniciar nosso serviço.
 
```bash
sudo systemctl start systemd-python.service
```
   
Agora nosso serviço está em execução, para validar isso utilizamos o serguinte comando:

  ```bash
sudo systemctl status systemd-python.service
```
  
Outros comando podem ser utilizados para controlar o seu novo serviço:
  
Para PARAR o serviço:
```bash
sudo systemctl stop systemd-python.service
```
Para REINICIAR o serviço:
  ```bash
sudo systemctl restart systemd-python.service
```
  
 **Nota**: Este processo não se aplica unicamente a scripts python. É possivel executar scripts de qualquer linguagem utilizando este método.
  
 **Referências**:
  https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units
  https://www.codementor.io/@ufukafak/how-to-run-a-python-script-in-linux-with-systemd-1nh2x3hi0e
  https://www.freedesktop.org/software/systemd/man/systemd.service.html
  https://medium.com/codex/setup-a-python-script-as-a-service-through-systemctl-systemd-f0cc55a42267
  
  
 
