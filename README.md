# O que é o MFetch-statusbar?

O Mfetch-statusbar é uma versão do MFetch feita para ser uma statusbar de i3, feita totalmente em bash puro e utilizando ferramentas do sistema Linux para 
mostrar informações como CPU, RAM, HDD (Armazenamento), rede (ON ou OFF), Bateria, data e hora.

## Dependências
* awk
* coreutils

Caso queira instalar:

```bash
sudo apt install coreutils mawk
```

## Como funciona?

O script, não desenha de fato as informações que irá mostrar da máquina, mas, quem mostra de fato é o próprio i3 em si.
O que o script faz de fato é apenas imprimir a cada segundo uma linha de JSON no stdout.

### CPU
Na coleta de CPU ele usa em porcentagem o uso de CPU que lê em /proc/stat

### RAM
Mostra o uso do total de bytes usado de RAM que lê em /proc/meminfo e bem ele lê utilizando o awk.

### Rede
Mostra apenas "ON" ou "OFF" que pega com base no que lê em /proc/net/route que no caso pergunta se existe uma rota padrão.

### HDD
Mostra o armazenamento do dispositivo, no caso mostra especificamente o espaço disponível do dispositivo... Usando o comando df.

### Bateria
Mostra especificamente a porcentagem da bateria que ele lê em /sys/class/power_supply/ que no caso lê um arquivo chamado "capacity".

### Data e hora
Bem... Usa um printf embutido no bash, sem nenhum comando externo.

## !AVISO!
O MFetch-statusbar foi feito exclusivamente para o i3, qualquer outra Window Manager que tentar utilizar, pode não funcionar.

## Instalação

```bash
git clone https://github.com/Ex3cutor76-V1/MFetch-i3status.git
cd MFetch-i3status/
sudo mv mfetch-statusbar /usr/local/bin/
```
Após fazer isso é recomendado também que você use
```
nano ~/.config/i3/config
```

E encontre a parte de "bar {" e coloque:

```bash
 bar {
    status_command mfetch-statusbar
}
```
E após isso você pode resetar o i3 usando `mod+shift+r` (Ou se caso você usa o DeByte Linux, use `mod+shift+c`)
