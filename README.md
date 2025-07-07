# Travalhoredes

Este projeto implementa 3 aplicativos (p1.py, p2.py, p3.py) para geração, envio, processamento e cálculo do determinante de matrizes em um ambiente com 3 VMs ou 3 máquinas distintas.

p1.py: Gera N matrizes aleatórias de ordem escolhida, e envia cada uma delas para o p2.py.

p2.py: Recebe uma matriz do p1.py, inverte (transposta) a matriz e envia para o p3.py.

p3.py: Recebe a matriz invertida, calcula o determinante e imprime os resultados.

Todos os programas usam a porta 6000/tcp para comunicação.

Pré-requisitos

Python 3 instalado em todas as máquinas.

As bibliotecas padrão do Python + numpy.

Instale o numpy com: pip install numpy

Execução passo a passo

Configuração da rede

Antes de iniciar, anote os endereços IP de cada máquina:

        IP da máquina onde roda o p2.py

        IP da máquina onde roda o p3.py

Você pode descobrir seu IP local usando o terminal da máquina: ip a

Instale o Docker

Como instalar o Docker no Ubuntu:

        Para utilizar o Docker em qualquer máquina é necessário instala-lo através do terminal da máquina usando o código: apt install docker.io 

        Para Windows ou macOS:

        Baixe de: https://www.docker.com/products/docker-desktop/

Obtendo os códigos através do Docker.

Para obter os códigos que estão no Docker é necessário fazer o download deles através do seguinte código no terminal:

sudo docker pull cordeiroprog/progx

x varia de 1 a 3 dependendo de qual programa você deseja baixar.

por exemplo: na máquina 1 vamos executar o p1:

sudo docker pull cordeiroprog/prog1

Inicie os aplicativos

Como nosso método de comunicação é TCP é importante que os programas sejam executados nessa sequência.

Máquina 3 (p3.py)

Execute o programa:

docker run -it –rm -p 6000:6000 cordeiroprog/prog3

Este ficará aguardando matrizes do p2.py indefinidamente.

Máquina 2 (p2.py)

Execute o programa:

docker run -it –rm -p 6000:6000 cordeiroprog/prog2

O programa perguntará:

Digite o IP do p3:

Digite o IP da máquina 3 e pressione ENTER.

Este ficará aguardando matrizes do p1.py e repassando para p3.py.

Máquina 1 (p1.py)

Execute o programa:

docker run -it –rm cordeiroprog/prog1

O programa perguntará:

Digite o IP do p2:

Digite a ordem da matriz quadrada:

Digite o número de matrizes a serem criadas:

Informe os valores solicitados.

O p1.py enviará as matrizes para o p2.py, que as processará e repassará para o p3.py.

Observações

        Os aplicativos podem ser interrompidos com Ctrl+C.

        O p2.py e o p3.py ficam rodando indefinidamente para receber novas matrizes.

