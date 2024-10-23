#ssh #infra #linux 

Com o SSH podemos realizar cópias de arquivos de nossa máquina para a máquina remota e vice-versa. Os exemplos a seguir partem do princípio que temos já temos acesso à máquina remota.

A cópia de arquivos é feita através do comando `SCP` (*security copy*) , que é um protocolo de rede para transferência de arquivos usando as proteção provida pelo SSH (*Secure Shell*). O comando tem a seguinte estrutura:

```bash
scp opcoes usuario_origem@IP_origem:arquivo_diretorio_origem usuario_destino@IP_destino::arquivo_diretorio_destino
```

No comando acima temos a estrutura básica de transferência de um arquivo ou diretório entre duas máquinas. Os parâmetros são o seguinte:

- `opcoes`: parâmetros opcionais para copia dos arquivos e/ou diretórios. Um dos parâmetros mais comuns é o parâmetro `-r`, que permite a cópia recursiva de diretórios.
- `usuario_origem`: o usuário da maquina de onde o arquivo será copiado.
- `IP_origem`: IP da maquina de onde o arquivo será copiado.
- `arquivo_diretorio_origem`: o arquivo/diretório em si que deve ser copiado.
- `usuario_destino`: usuário da máquina destino do arquivo/diretório
- `IP_destino`: IP do servidor de destino do arquivo/diretório
- `arquivo_diretorio_destino`: diretório de destino do arquivo

No caso de cópia DE ou PARA nossa máquina local, podemos omitir o usuário e o IP e indicar apenas o diretório de destino. Por exemplo, vamos supor a cópia de um arquivo de um servidor remoto para o diretório *download* nossa máquina:

```bash
scp usuario_servidor@IP_servidor:/mnt/backup/arquivo_backup.zip ~/Downloads
```

Mais informações em:

[Como Usar Comando SCP para Transferir Arquivos no Linux](https://www.hostinger.com.br/tutoriais/usar-comando-scp-linux-para-transferir-arquivos)